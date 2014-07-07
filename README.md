declarative-module-pattern
==========================

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

Declarative Module Pattern

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

