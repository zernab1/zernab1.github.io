---
layout: post
title: Pandas Refresher
---

Ah, I took a break from the daily posting for this weekend. I think referring to this as a "100daysofcode" challenge is not accurate anymore haha.

Anyway, today I wanted to review some pandas basics, which feels rudimentary but at the same time I've been worried that copy-pasting basic solutions has been causing me to not truly remember syntax. I want to make sure I *do* understand, in case I have to implement something or speak on it without access to online resources in an interview.

Not so much memorization, but more so a better grasp on the fundamentals. Following along 'Intro to Pandas' on Leetcode and I have been truly humbled, lol. Yall, tell me why I forgot the syntax for passing in headers for DataFrames🤦‍♂️

I was here trying 
`df = pd.DataFrame(student_data)`

Which doesn't cause an exception, but they were expecting column headers to be passed. Which ended up being:
`df = pd.DataFrame(student_data, columns=['student_id', 'age'])`

Anyway, I'm being a little hard on myself. I remembered to use .head() to get the first however-many-number-of-rows-you-need to get from your df, (by default it's 5 rows). I also remembered you use .shape to get the size of a DataFrame... Just forgot that it was an attribute and not a method, and that you can access the number of rows/col by indexing the shape attribute
`return [df.shape[0], df.shape[1]]`

The older I get, the more important I find referring to official library docs (vs looking for how to resources online that might give you the answer in a nice, quick, bite-sized solution you can copy-paste). I use to read documentation as a last resort, haha. Just because of how many more resources are online that piece meal that same information and make it easier to quickly use. 

But when it comes to learning, I think reffering to documentation is the way to go. So here I am, in the pandas [docs](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.loc.html) learning about how to select data from a df using the `loc()` attribute. It can be used to perform boolean indexing that represents the condition where a certain column is equal to a condition you want. This one Leetcode wanted a condition wrote out that selected only the student with an id=101.

My answer ended up looking like this
`def selectData(students: pd.DataFrame) -> pd.DataFrame:`
    `students = students.loc[students['student_id'] == 101, ['name', 'age']]`
    `return students`

And adding a column to an existing df isn't complicated at all, you literally just give it the name of the new column in [""] and it creates it. If you give it only one value, then pandas populates all rows in your dataframe with that value for that new column. If you give more, but it doesn't match the number of rows in your dataframe it *will* raise a ValueError at you, lol.

You can do cool things like use an existing column to create a new one, and do some arithmetic on it. Like this example:
`employees['bonus'] = 'employees['salary'] * 2'`
creates a **bonus** column that is simply the salary column for all employees doubled. Man wouldn't that be a nice bonus :/

Or change the datatype of an existing columnm, say for some reason you want to change the bonus to be a whole number and not a float, if that was what its datatype was before: 
`employees['bonus'] = employees['bonus'].astype(int)`

Anyway, also learned about the `drop_duplicates()` method for df's, that you can use to get rid of duplicates values. If you want to get rid of duplicate values on just one column (say emails, for example), you do `df = df.drop_duplicates(subset=['email'])`

Another good df method to know is `dropna`, which you can use in a similar way as `drop_duplicates` and get rid of records that contain na values only for particular columns you specify.

You can also use `fillna()` to instead of dropping, you replace the na with a default value (like 0, for example):
`employees['address'].fillna('-', inplace=True)`

Also learned how to rename columns in a df today, you use the `rename()` method, like so:
`students = students.rename(columns={'id': 'student_id'})`
But don't forget that if you don't add a `inplace=True` argument to that method, that you won't be able to change the df in-place. For example:
`students.rename(columns={'id': 'student_id'})`
would leave the students dataframe unchanged.

Alright, what if you have two dataframes and you want to combine them? There's this method called `.concat()`, and you can use it to either vertically or horizontally combine df. By default it's vertical, meaning it appends the df2 to the end of the first df. Say you have
| student_id | name |
| ----------- | ----------- |
| 1 | Mason |
| 2 | Ava |

And you want to combine it with this dataframe, that contains the same columns 
| student_id | name |
| ----------- | ----------- |
| 3 | Lauren |
| 4 | Bill |
| 5 | Jill |

You would do `df3 = pd.concat([df1, df2], ignore_index=True)`

By default the axis=0, for vertical. But if you were adding on new columns with data to a df, you would set axis=1.

---

Keeping these posts short is probably the key way to stay consistent with posting, (and also to prevent from taking too much time away from the actual learning process). So that's it for now! Til next time~











