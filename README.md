definitive-module-pattern
==========================

The "Definitive Module Pattern" is an alternative to the "Module Pattern" and the "Revealing Module Pattern". It offers the following advantages: declaratively namespaces the private and public subroutines, decouples the public subroutines from the return statement, and groups all content within object literals.

Module Pattern

    var module = (function () {

        // private subroutines
        var private_one = function () {};
        var private_two = function () {};

        // public subroutines
        return {
            private_one: function () {
                private_one();
            },
            private_two: function () {
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
            private_one: private_one,
            private_two: private_two
        };

    })();

Definitive Module Pattern

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

