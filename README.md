Javascript - Definitive Module Pattern
==========================

http://inniepress.blogspot.com/2014/07/definitive-module-pattern.html

The Javascript "Definitive Module Pattern" (DMP) is an alternative to the "Module Pattern" (MP) and the "Revealing Module Pattern" (RMP). It offers the following advantages: declaratively namespaces the private and public functions, decouples the public functions from the return statement, groups all functions within object literals, and offers configurable public scopes (or polyscopes).

    // Definitive Module Pattern
    var module = (function () {
    
        // private
        var _private = {
            privateOne: function () {},
            privateTwo: function () {}
        };
    
        // public
        var _public = {
            publicOne: _private.privateOne,
            publicTwo: _private.privateTwo
        };
    
        return _public;
    
    })();

DMP is better than RMP, because it's declarative. It's easier to see which function-methods are private and which function-methods are public - like the keywords found in Java, C++, and other static languages.

**Using private functions as a property of `_private` Object Literal?**  
All function-methods are bundled under a single object literal, which is labeled as `_private`. DMP therefore is more object-oriented (and less procedural ) than RMP. It's also declarative - anyone who looks at the code knows that the `_private` object contains private data.

**Decoupling the public functions from the return statement?**  
RMP couples the `return` statement to an object literal (which contains the public function-methods), and it looks messy (like writing all your code on a single line). It's declarative, and easier, to return a variable named `_public`.

**Configurable public scopes?**  
Let's say you want to provide one set of public function-methods for your module (a & b), and another set of public function-methods for your module (a & c). The user can therefore select which configuration of public function-methods they need from your module. DMP makes it easier to declare public scopes when the `return` statement has been decoupled from the object literal. See the code under "configurable public scopes" for further understanding.

==========================

Module Pattern

    var module = (function () {

        // private
        var privateOne = function () {};
        var privateTwo = function () {};

        // public
        return {
            publicOne: function () {
                privateOne();
            },
            publicTwo: function () {
                privateTwo();
            }
        };

    })();

Revealing Module Pattern

    var module = (function () {

        // private
        var privateOne = function () {};
        var privateTwo = function () {};

        // public
        return {
            publicOne: privateOne,
            publicTwo: privateTwo
        };

    })();

**Definitive Module Pattern**

    var module = (function () {

        // private
        var _private = {
            privateOne: function () {},
            privateTwo: function () {}
        };

        // public
        var _public = {
            publicOne: _private.privateOne,
            publicTwo: _private.privateTwo
        };

        return _public;

    })();

Definitive Module Pattern (CoffeeScript version)

    module = (->

        // private
        _private =
            privateOne: ->
            
            privateTwo: ->
            
    
        // public
        _public =
            publicOne: _private.privateOne
            publicTwo: _private.privateTwo
    
        _public
    )()

Definitive Module Pattern (CommonJS version)

    var module = (function () {

        // private
        var _private = {
            privateOne: function () {},
            privateTwo: function () {}
        };

        // public
        var _public = {
            publicOne: _private.privateOne,
            publicTwo: _private.privateTwo
        };

        return _public;

    })();

    module.exports = module;


Definitive Module Pattern (configurable public scopes)

    var module = (function () {

        // private
        var _private = {
            privateOne: function () {},
            privateTwo: function () {},
            privateThree: function () {}
        };

        // public (set 1)
        var _public1 = {
            publicOne: _private.privateOne,
            publicTwo: _private.privateTwo
        };

        // public (set 2)
        var _public2 = {
            publicOne: _private.privateOne,
            publicThree: _private.privateThree
        };

        // configurable public scopes
        var _publics = [_public1, _public2];

        return _publics;

    })();
