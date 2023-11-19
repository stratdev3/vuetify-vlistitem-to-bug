<template>
    <v-container>

        <!-- DESCRIPTION -->
        <h1>
            Change behaviour
        </h1>
        <p>
            <strong>Affect</strong> : <code>v-list-item</code>, <code>v-select</code> and possibibly others
        </p>
        <p><strong>Cause</strong> :</p>
        <ol class="ml-12">
            <li>
                when using the <code>to</code> property on a <code>v-list-item</code>,
                vuetify 3 use the <code>vue-router/RouterLink.useLink()</code>
                to detect if the property is the same as the current route in URL.
            </li>
            <li>
                Due to a <a href="https://router.vuejs.org/guide/migration/#Removal-of-the-exact-prop-in-router-link-">vue-router 4.x breaking change</a>,
                routes are compared with only their <code>path</code> excluding <code>query</code>.
            </li>
        </ol>
        <p class="mt-4"><strong>Reproduce step </strong> : in the example bellow, only the <em>Current</em> item should have active class, not all.</p>

        <!-- CODE -->
        <v-row>
            <v-col col=6>

                <v-select
                    :items="items"
                    :model-value="item_selected"
                    menu
                    label="error all items actives"
                    class="mt-10">
                    <template #item="{ props, item }">
                        <v-list-item v-bind="{ ...props, title: '', to: item.raw.value }">
                            <v-list-item-title>
                            {{ item.raw.title }}
                            </v-list-item-title>
                        </v-list-item>
                    </template>
                </v-select>

            </v-col>
        </v-row>
    </v-container>
</template>

<script>
export default {
    computed: {
        items: function() {
            return [
                { title:'All', value: '/home?query=' },
                { title:'Archive', value: '/home?query=usr_date+is+previous' },
                { title:'Current', value: '/home?query=usr_date+is+in' },
                { title:'Next', value: '/home?query=usr_date+is+next' },
            ];
        },
        item_selected: function() {
            return { title:'Current', value: '/home?query=usr_date+is+in' };
        },
    }
}
</script>