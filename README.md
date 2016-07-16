# Visual Studio Dark Theme for EnlighterJS

This theme tries to match the Dark theme of Visual Studio as close as possible for C# and XML.

However, it is not possible to match everything 100% correctly with regex only, so some class and enum usage in code might be incorrect. The matching is also dependent on correct namning of classes (PascalCase), interfaces (IPascalCase) and generics (T or TPascalCase).

## Notes

**Only tested with C# and XML**.

This is tested for use with [EnlighterJS](http://enlighterjs.org/) v2.10.1 and [the Wordress Plugin](https://wordpress.org/plugins/enlighter/) v3.1.

This also requires some modifications to EnlighterJS for better matching of keywords etc. in C#, which is why I have included it is in this project as well - you can hower do the modifications yourself.

## Changes to EnlighterJS (C#)

I've added more words to the keywords and changed alias for the primitives. I've also added regex patterns for classes, interfaces, operators and numbers to be able to match the theme of Visual Studio as close a possible.

```Javascript
EJS.Language.csharp = new Class({
Extends: EJS.Language.generic,
setupLanguage: function() {
    this.keywords = {
        keywords: {
            csv: "as, base, break, case, catch, checked, continue, default, do, else, event, explicit, false, finally, fixed, for, foreach, goto, if, implicit, internal, is, lock, namespace, new, null, operator, params, private, protected, public, ref, return, sizeof, stackalloc, switch, this, throw, true, try, typeof, unchecked, using, void, while, abstract, async, class, const, delegate, dynamic, event, extern, in, interface, out, override, readonly, sealed, static, unsafe, virtual, volatile",
            alias: "kw1"
        },
        primitives: {
            csv: "bool, byte, char, decimal, double, enum, float, int, long, sbyte, short, struct, uint, ulong, ushort, object, string, var",
            alias: "kw1"
        }
    };
    this.patterns = {
        classes: {
            pattern: /\s*:\s*([A-Z]\w+)(?=[$\s<])|<([A-Z][^A-Z]\w*)>|\[([A-Z]\w+)[(\]]|(?:\(|\(this\s|,\s)([A-Z]\w+)(?!\s=)(?:\s|\.)|(?:new|return)\s([A-Z]\w+)[$\s(<]|(?:public|private|protected)\s(?:static\s|sealed\s|override\s|virtual\s)?(?:readonly\s|const\s|class\s)?([A-Z]\w+)|\(([A-Z]\w+\))|as\s([A-Z]\w+)/gm,
            alias: "kw3"
        },
        interfaces: {
            pattern: /(?:\(|\s)(I[A-Z]\w+)|enum\s([A-Z]\w+)|<(T|T[A-Z]\w*?)>/gm,
            alias: "kw4"
        },
        operators: {
            pattern: /\+|\-|\*|\/|\|{1,2}|&{1,2}|[\+\-\*\/]?=/gim,
            alias: "sy0"
        },
        slashComments: {
            pattern: this.common.slashComments,
            alias: "co1"
        },
        multiComments: {
            pattern: this.common.multiComments,
            alias: "co2"
        },
        chars: {
            pattern: this.common.singleQuotedString,
            alias: "st0"
        },
        strings: {
            pattern: this.common.doubleQuotedString,
            alias: "st1"
        },
        numbers: {
            pattern: /\b((([0-9]+)?\.)?[0-9_]+([e][-+]?[0-9]+)?|0x[A-F0-9]+|0b[0-1_]+)\b/gim,
            alias: "nu0"
        },
        brackets: {
            pattern: this.common.brackets,
            alias: "br0"
        },
        methodCalls: {
            pattern: this.common.methodCalls,
            alias: "me1"
        }
    };
}
});
```
