Javascript - Definitive Module Pattern
==========================

http://inniepress.blogspot.com/2014/07/definitive-module-pattern.html

The Javascript "Definitive Module Pattern" is an alternative to the "Module Pattern" and the "Revealing Module Pattern". It offers the following advantages: declaratively namespaces the private and public functions, decouples the public functions from the return statement, groups all functions within object literals, and offers configurable public scopes (or polyscopes).

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
            private_two: function () {}
        };

        // public (set 1)
        var _public1 = {
            public_one: _private.private_one,
            public_two: _private.private_two
        };

        // public (set 2)
        var _public2 = {
            public_one: _private.private_one,
            public_two: _private.private_two
        };

        // configurable public scopes
        var _publics = [_public1, _public2];

        return _publics;

    })();
