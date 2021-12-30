# TypeScript (TS) and React
This guide builds on top of the main guidelines, with TypeScript/React-specific additions.

## Files
  * TypeScript files end with the file extension `.ts`.
  * React files end with the file extension `.tsx`.

Classes, interfaces, enums in files:
* **In a TypeScript-only project**: There should only be 1 class per file. Type aliases and interface declarations should be together in a single file.
* **In a TypeScript+React project**: The component props and class/function props should be together in one file.

Related functions should be together in a single file. This is left up to a developer to decide.

## Naming convention
  *  `PascalCase`: classes, interfaces, types, enums, decorators, and type parameters
  * `lowerCamelCase`: variables, functions, and parameters
  * `SCREAMING_CASE`: constants

Abbreviations should use `PascalCase`. The first letter is capitalized, and the rest are lowercase.
However, if the abbreviation is two-letters long, like IO (input/output), both letters are capitalized.
  * `HttpRequest`
  * `IOStreamReader`
  * `UserId`

If possible, try to avoid abbreviations and acronyms, since it can be confusing. Generally, they should only
be used if it is well-known within the domain. Examples include:
  * **API**: *Application Programming Interface*
  * **REST**: *Representational State Transfer*
  * **URI**: *Uniform Resource Identifier*
  * **L10N**: *Localization*

```ts
// good
let customerId = 8000;
let httpRequest = request.get('/customers/' + customerId);

// bad
let cstmrId = 8000;
let hreq = request.get('/customers/' + cstmrId);
```

## Comments
There are two types of comments:
  * Multiline comments: `/** ... */`
  * Single-line comments: `//...`

Multiline comments must use [TSDoc](https://tsdoc.org/) - a documentation standard for TypeScript.
  * To document a function, include a one-sentence summary, one space after the start.
    Optionally, include a description (with a newline after the summary) that includes any details needed.
  * Include any TSDoc annotations necessary, like `@param` and `@return`.

We use the following annotations, in the given order:
  * `@example`
  * `@deprecated` / `@experimental`
  * `@link` / `@see`
  * `@typeParam`
  * `@param`
  * `@returns`
  * `@throws`

Do not include the type of the parameter in `@param` annotations. The type is already included in the function signature.

An example function might look like:
```ts
/**
 * @param array - collection of items to iterate over
 * @param callback - a function to apply over each item in the array
 * @returns the result of the callback function
 */
export function map<T>(array: T[], callback: (item: T, index: number, array: T[]) => T): T[] {
	let map = [];
	for(let i = 0; i < array.length; i++) {
		map.push(callback(array[i], i, array));
	}
	return map;
}
```

## Equality
Use triple-equality (strict equality) `===` and `!==` for type checking, to avoid surprising implicit type coercions.

## Collections
To iterate over an array, use the `for...of` loop. This is preferred over `for...in`,since `for...in`
also iterates over the properties and functions of the object.

Use the indexing for loop only when you need access to the index of the item. Otherwise, `for...in` is the default.

```ts
for(let i = 0; i < array.length; i++) {
	// code...
}
```

## Variables
Use `let` or `const` to define variables; avoid using `var`.
  * `var` is either globally scoped, function scoped.
  * `let` is block scoped.

It is important to note that in JavaScript, `const` is **not** immutable. The reference is immutable, so primitive values in constants are immutable. This is not the case for objects, like arrays. A constant cannot be reassigned or re-declared.