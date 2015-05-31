Javascript - Definitive Module Pattern
==========================

http://inniepress.blogspot.com/2014/07/definitive-module-pattern.html

The Javascript "Definitive Module Pattern" (DMP) is an alternative to the "Module Pattern" (MP) and the "Revealing Module Pattern" (RMP). It offers the following advantages: declaratively namespaces the private and public functions, decouples the public functions from the return statement, groups all functions within object literals, and offers configurable public scopes (or polyscopes).

    var module = (function () {
    
        // private
        var _private = {
            private_one: function () {},
            private_two: function () {}
        };
    
        // public
        var _public = {
            public_one: _private.private_one,
            public_two: _private.private_two
        };
    
        return _public;
    
    })();

DMP is better than RMP, because it's declarative. It's easier to see which function-methods are private and which function-methods are public - like the keywords found in Java, C++, and other static languages.

**Using private functions as a property of `_private` Object Literal?**  
All function-methods are bundled under a single object literal, which is labeled as `_private`. DMP therefore is more object-oriented (and less procedural ) than RMP. It's also declarative - anyone who looks at the code knows that the `_private` object contains private data.

**Decoupling the public functions from the return statement?**  
The RMP couples the return statement to an object literal (which contains the public function-methods) - it looks messy (like writing all your code on a single line). It's declarative, and easier, to return a variable named `_public`.

**Configurable public scopes?**  
Let's say you want to provide one set of public function-methods for your module (a & b), and another set of public function-methods for your module (a & c). The user can therefore select which configuration of public function-methods they need from your module. DMP makes it easier to declare public scopes when the `return` statement has been decoupled from the object literal. See the code under "configurable public scopes" for further understanding.

==========================

Module Pattern

    var module = (function () {

        // private
        var private_one = function () {};
        var private_two = function () {};

        // public
        return {
            public_one: function () {
                private_one();
            },
            public_two: function () {
                private_two();
            }
        };

    })();

Revealing Module Pattern

    var module = (function () {

        // private
        var private_one = function () {};
        var private_two = function () {};

        // public
        return {
            public_one: private_one,
            public_two: private_two
        };

    })();

**Definitive Module Pattern**

    var module = (function () {

        // private
        var _private = {
            private_one: function () {},
            private_two: function () {}
        };

        // public
        var _public = {
            public_one: _private.private_one,
            public_two: _private.private_two
        };

        return _public;

    })();

Definitive Module Pattern (CoffeeScript version)

    module = (->

        // private
        _private =
            private_one: ->
            
            private_two: ->
            
    
        // public
        _public =
            public_one: _private.private_one
            public_two: _private.private_two
    
        _public
    )()

Definitive Module Pattern (CommonJS version)

    var module = (function () {

        // private
        var _private = {
            private_one: function () {},
            private_two: function () {}
        };

        // public
        var _public = {
            public_one: _private.private_one,
            public_two: _private.private_two
        };

        return _public;

    })();

    module.exports = module;


Definitive Module Pattern (configurable public scopes)

    var module = (function () {

        // private
        var _private = {
            private_one: function () {},
            private_two: function () {},
            private_three: function () {}
        };

        // public (set 1)
        var _public1 = {
            public_one: _private.private_one,
            public_two: _private.private_two
        };

        // public (set 2)
        var _public2 = {
            public_one: _private.private_one,
            public_three: _private.private_three
        };

        // configurable public scopes
        var _publics = [_public1, _public2];

        return _publics;

    })();
