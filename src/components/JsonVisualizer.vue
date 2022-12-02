<template>
    <div :class="target"></div>
</template>

<script>
export default {
    props: ["data", "target"],
    data() {
        return {
            templates: {},
            collapsible: false
        }
    },
    mounted() {
        var json = this.data
        var el = document.querySelector("." + this.target);
        el.innerHTML = this.jsonViewer(json, true);
    },
    updated() {

        var json = this.data
        var el = document.querySelector("." + this.target);
        el.innerHTML = this.jsonViewer(json, true);

    },
    methods: {
        jsonViewer(json, collapsible = false) {
            this.collapsible = collapsible;
            this.templates = {
                item:
                    '<div class="json__item"><div class="json__key">%KEY%</div><div class="json__value json__value--%TYPE%">%VALUE%</div></div>',
                itemCollapsible:
                    '<label class="json__item json__item--collapsible"><input type="checkbox" class="json__toggle"/><div class="json__key">%KEY%</div><div class="json__value json__value--type-%TYPE%">%VALUE%</div>%CHILDREN%</label>',
                itemCollapsibleOpen:
                    '<label class="json__item json__item--collapsible"><input type="checkbox" checked class="json__toggle"/><div class="json__key">%KEY%</div><div class="json__value json__value--type-%TYPE%">%VALUE%</div>%CHILDREN%</label>'
            };

            return this.parseObject(json);
        },
        createItem(key, value, type) {
            var element = this.templates.item.replace("%KEY%", key);

            if (type == "string") {
                element = element.replace("%VALUE%", '"' + value + '"');
            } else {
                element = element.replace("%VALUE%", value);
            }

            element = element.replace("%TYPE%", type);

            return element;
        },
        createCollapsibleItem(key, value, type, children) {
            var tpl = "itemCollapsible";
            var element = this.templates.itemCollapsible.replace("%KEY%", key);

            if (this.collapsible) {
                tpl = "itemCollapsibleOpen";
                element = this.templates.itemCollapsibleOpen.replace("%KEY%", key);
            }



            element = element.replace("%VALUE%", type);
            element = element.replace("%TYPE%", type);
            element = element.replace("%CHILDREN%", children);

            return element;
        },
        handleItem(key, value) {
            var type = typeof value;

            if (typeof value === "object") {
                return this.handleChildren(key, value, type);
            }

            return this.createItem(key, value, type);
        },
        handleChildren(key, value, type) {
            var html = "";

            for (var item in value) {
                var key = item,
                    val = value[item];

                html += this.handleItem(key, val);
            }

            return this.createCollapsibleItem(key, value, type, html);
        },
        parseObject(obj) {
            var result = '<div class="json">';

            for (var item in obj) {
                var key = item,
                    value = obj[item];

                result += this.handleItem(key, value);
            }

            result += "</div>";

            return result;
        }
    },
}
</script>

<style >
@import url("https://fonts.googleapis.com/css?family=Source+Code+Pro");

.json {
    font-family: "Source Code Pro", monospace;
    font-size: 16px;
}

.json>.json__item {
    display: block;
}

.json__item {
    display: none;
    margin-top: 10px;
    padding-left: 20px;
}

.json__item--collapsible {
    cursor: pointer;
    overflow: hidden;
    position: relative;
}

.json__item--collapsible::before {
    content: "+";
    position: absolute;
    left: 5px;
}

.json__item--collapsible::after {
    background-color: lightgrey;
    content: "";
    height: 100%;
    left: 9px;
    position: absolute;
    top: 26px;
    width: 1px;
}

.json__item--collapsible:hover>.json__key,
.json__item--collapsible:hover>.json__value {
    text-decoration: underline;
}

.json__toggle {
    display: none;
}

.json__toggle:checked~.json__item {
    display: block;
}

.json__key {
    color: darkblue;
    display: inline;
}

.json__key::after {
    content: ": ";
}

.json__value {
    display: inline;
}

.json__value--string {
    color: green;
}

.json__value--number {
    color: blue;
}

.json__value--boolean {
    color: red;
}
</style>