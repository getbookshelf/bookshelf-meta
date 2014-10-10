# Bookshelf PHP Coding Standards

The Bookshelf project intends to establish common coding standards to allow for consistency.  
This document defines the coding standards for the PHP programming language.

## General Notes
The intention of this document is to provide a guideline to the developer. In some cases, it may however be more appropriate to differ from them. This is up to the developer to judge. The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

Bookshelf not only intends to specify their own guidelines but also to comply with official standards. Therefore, these guidelines are based on the [PHP FIG Standards](https://github.com/php-fig/fig-standards). Do note however that there are some differences.

Indented fragments provide examples.

	This is an example of an indented fragment providing an example.

## Guidelines Regarding Object Oriented Development
### Namespaces
Namespace and class names MUST have the following structure:

	\Bookshelf\[Namespace name]\[Class name]
	
Namespace and class names MUST only use ASCII letters and be written in upper camel case ("PascalCase").

	\Bookshelf\ExternalApi\GoogleBooksApiRequest
	
On the filesystem, each segment of the namespace MUST be converted to a separate directory and the extension `.php` MUST be appended to the class name.

	/Bookshelf/ExternalApi/GoogleBooksApiRequest.php
	
### Autoloading
Bookshelf provides an `autoload.php` that SHOULD be used in every file to have the necessary classes loaded automatically. The file is found in `/lib/vendor/autoload.php`.  
An example would be:

	require __DIR__ . '/lib/vendor/autoload.php';
	
## Coding Guidelines
The following example encompasses the most important rules as a quick overview:

	<?php
	
	namespace \Bookshelf\ExternalApi;
	
	use \Bookshelf\DataType;
	use \Bookshelf\DataIo\DatabaseConnection;
	
	class GoogleBooksApiRequest extends ExternalApiRequest {
		public function sampleRequest($some_variable, $another_variable = 'default value') {
			if($some_variable == $another_variable) {
				$this->someMethod();
			}
			elseif(strtolower($some_variable) == $another_variable) {
				// TODO: Show warning to the user
			}
			else {
				echo 'Some message to the user.';
			}
		} 
	}

### Files
Files MUST only use `<?php` (resp. `?>`).

Files MUST only use UTF-8 without BOM.

All files MUST use the Unix Line Feed ending.

All files MUST end with a single blank line.

The closing `?>` tag MUST be omitted from files containing only PHP.

### Constants
Class constants MUST be declared in all upper case with underscore separators.

	const VERSION_CODE = 1;

If a class constant needs to be set to an expression, `define()` MAY be used.  
The name used for `define()` SHOULD be the constant name in lower case and without separators.

	define('rootdir'), __DIR__ . '/../../../../');
	
	class Application {
		const ROOT_DIR = rootdir;
	}

### Indenting
Code SHOULD be indented to improve readability.

Code MUST be indented only with 4 spaces and MUST NOT be indented with tabs.

### Keywords and PHP Constants
PHP keywords and constants MUST be in lower case.

	$some_bool = false;
	$my_var = null;
	
	exit();

### Namespace and Use Declarations
There MUST be one blank line before and after the `namespace` declaration.

The `use` declarations MUST go after the `namespace` declaration.

There MUST be one blank line after the `use` declarations.

### Classes
The `extends` and `implements` keywords MUST be declared on the same line as the class name.

The opening brace for the class MUST be on the same line as the class name. The closing brace for the class MUST go on the next line after the body.

	class SomeClass extends ParentClass implements \Countable {
		// class definition
	}

### Properties
Visibility MUST be declared on all properties.

There MUST NOT be more than one property declared per statement.

Property names MUST be declared in Snake Case.

Property names SHOULD NOT be prefixed to indicate visibility or data type.

	public $cover_image;
	private $user;

### Methods
Visibility MUST be declared on all methods.

Property names SHOULD NOT be prefixed to indicate visibility or return type.

Method names MUST be declared in Camel Case.

Method names MUST NOT be declared with a space after the method name. The opening brace MUST NOT go on its own line, and the closing brace MUST go on the next line following the body. There MUST NOT be a space after the opening parenthesis, and there MUST NOT be a space before the closing parenthesis.

In the argument list, there MUST NOT be a space before each comma, and there MUST be one space after each comma.

Method arguments with default values MUST go at the end of the argument list.

	public function volumeSearch($q, $limit = 0) {
		// function definition
	}
	
### Method Calls
When making a method or function call, there MUST NOT be a space between the method or function name and the opening parenthesis, there MUST NOT be a space after the opening parenthesis, and there MUST NOT be a space before the closing parenthesis. In the argument list, there MUST NOT be a space before each comma, and there MUST be one space after each comma.

	$database_connection->executeQuery($query);
	volumeSearch($q, 3);
	
### Strings
Strings MUST only be declared with double quotes `"` if they include expressions. Otherwise, single quotes `'` MUST be used.

Variables in double quote strings SHOULD be wrapped in curly brackets to avoid parsing errors.

	$my_string = 'Hello, World.';
	$personal_string = "Hello, {$user}.";

### Ternary operators
In order to make the code more efficient, the ternary operator SHOULD be used, when an immediate conditional return is needed.

The ternary SHOULD be enclosed by round brackets to ensure readability and minimize error probability. There also MUST be a space before and after `?` and  `:`.
After the opening and before the closing bracket though, there MUST NOT be a space.

    echo 'Some variable: ' . (empty($some_variable) ? 'Nothing' : $some_variable);

### `if` Statements
An `if` statement MUST look like the following:

	if($some_variable == $another_variable) {
		$this->someMethod();
	}
	elseif(strtolower($some_variable) == $another_variable) {
		// TODO: Show warning to the user
	}
	else {
		echo 'Some message to the user.';
	}

If an small `if` statement only encloses one line with no `else` or `elseif` statement following, it SHOULD only use one line.
Such one-line statements MUST ommit the curly brackets. There MUST be a space after the closing bracket of the one-line `if` statement.

    if($some_variable == $another_variable) echo 'They\'re equal';

### `switch case` Statements
A `switch case` statement MUST look like the following. There MUST be a comment (like `// no break`) when fall-through is intentional.

	switch($expression) {
		case 0:
			echo 'That was a zero.';
			break;
		case 1:
			// no break
		case 2:
		default:
			echo 'Default case';
	}

### Loops
`for`, `foreach` and `while` loops MUST look like the following:

	for($i = 0; $i < 42; $i++) {
		// body
	}
	
	foreach($iterable as $key => $value) {
		// body
	}
	
	while($expression) {
		// body
	}
	
### `require`, `include`
`require_once` and `include_once` SHOULD be used if a file is not supposed to be included more than once.

`require`, `include`, `require_once` and `include_once` MUST only be used like in the following example. Note the omission of the brackets.

	require Application::ROOT_DIR . 'config.php';

### Comments
Comments SHOULD only be used to explain program behavior that is unexpected. Code that can easily be understood SHOULD NOT be commented.


Comments declared with `//` MUST be indented by one space and MUST NOT follow directly after the leading slash.

The `TODO` keyword MAY be used.

	// implemented according to https://developers.google.com/books/docs/v1/using#PerformingSearch
	
	// TODO: Change according to coding standards

### Abbreviations
Abbreviations SHOULD NOT be used in class, property and method names to increase readability.

Abbreviations MUST be treated like words for naming conventions.

	class GoogleBooksApiRequest { // Note that Api is not spelled API
		// class body
	}