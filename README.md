Javascript - Definitive Module Pattern
==========================

http://inniepress.blogspot.com/2014/07/definitive-module-pattern.html

The Javascript "Definitive Module Pattern" is an alternative to the "Module Pattern" and the "Revealing Module Pattern". It offers the following advantages: declaratively namespaces the private and public functions, decouples the public functions from the return statement, groups all functions within object literals, and offers configurable pubic scopes (or polyscopes).

Module Pattern

    var module = (function () {

        // private subroutines
        var private_one = function () {};
        var private_two = function () {};

        // public subroutines
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

        // private subroutines
        var private_one = function () {};
        var private_two = function () {};

        // public subroutines
        return {
            public_one: private_one,
            public_two: private_two
        };

    })();

**Definitive Module Pattern**

    var module = (function () {

        // private subroutines
        var _private = {
            private_one: function () {},
            private_two: function () {}
        };

        // public subroutines
        var _public = {
            public_one: _private.private_one,
            public_two: _private.private_two
        };

        return _public;

    })();

Definitive Module Pattern (CommonJS version)

    var module = (function () {

        // private subroutines
        var _private = {
            private_one: function () {},
            private_two: function () {}
        };

        // public subroutines
        var _public = {
            public_one: _private.private_one,
            public_two: _private.private_two
        };

        return _public;

    })();

    module.exports = module;


**Definitive Module Pattern (Poly-public Version)**

    var module = (function () {

        // private scope
        var _private = {
            private_one: function () {},
            private_two: function () {}
        };

        // public scope 1
        var _public1 = {
            public_one: _private.private_one,
            public_two: _private.private_two
        };

        // public scope 2
        var _public2 = {
            public_one: _private.private_one,
            public_two: _private.private_two
        };

        // configurable poly-public scope
        var _publics = [_public1, _public2];

        return _publics;

    })();

    module.exports = module;
