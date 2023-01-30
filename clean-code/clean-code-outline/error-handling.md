# Error Handling

### Two types of exceptions

* Expected or business exceptions ~ _checked?_
* Unexpected program or environment errors ~ _unchecked?_

### Good Practices

* Prefer exceptions to return codes - _decreases pollution of clients_
* Prefer exception types to exception payload - _error codes_
* Provide context for exception:
  * chain exceptions when wrapping
  * add erroneous object\(s\)
* Do not return null - _throw exception \(e.g. IllegalArgumentException\)_
* Prefer runtime exceptions to checked exceptions - _decreases pollution and dependency_
* Wrap exceptions in module or service specific exceptions - _decrease dependency_
* Only unexpected exceptions should be logged on error level with stack-trace.

### Bad Practices

* Swallow exceptions
* Implement business logic in catch block
* Do not catch exceptions unless you handle them
* `handleError()` type of methods - 
  * _not readable what they do_
  * _they cheat the compiler too_



