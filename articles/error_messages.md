# Error Messages

A good error message can turn what would be a day of debugging into a five minute fix, but there is very little guidelines on how to write a good error message out there.
There are good examples and bad examples out there and there are pieces of advice you can find scattered around but there are no unified guides or templates.

## The content of a good error message

The long-term goal of this article is to compile ideas and advice on error messaging, as well as a group of templates and patterns that can be used to improve error messages.
As a start, these are what I think are the most important aspects of an error message:

1. It identifies what part of the input (or environment) caused the error.
2. It states why the error occurred.
   a. Ideall,y it states the condition that was not met and the value that did not meet that condition, i.e. "list must have less than 5 elements, 87 elements provided"
3. It tells the caller what they need to change to prevent the error on the next call.

Error messages should therefore have the structure `"{pointer to error in input}: {reason the error occurred}. {solution}."`. For example, 
`"invalid param 'age': 'age' must be between 0 and 150 (inclusive), age provided was 155. Age can be set to null if it is not relevant to this use case."`.

The template should not be taken too strictly. If it wasn't for the undefined case the `{solution}` part of the template would not be necessary, we could just write
`"invalid param 'age': 'age' must be between 0 and 150 (inclusive), age provided was 155"` since the solution is implied by the reason `"must be between 0 and 150"`. The order and format
are also not important, we could use the same principles in a JSON response:

```json
{
  "pointer": "/data/user/age",
  "error": "`/data/user/age` must be between 0 and 150, age provided was 155. Age can be set to `null` if it is not relevant to this use case."
}
```
