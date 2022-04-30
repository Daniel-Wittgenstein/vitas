<template>



    <q-layout view="hHr LpR lFf">
        <q-header elevated>
            <q-toolbar>


<!--
                <q-btn
                    flat
                    dense
                    round
                    icon="menu"
                    aria-label="Menu"
                    @click="toggleLeftDrawer"
                />

-->


                <q-toolbar-title>
                    Miezer
                </q-toolbar-title>

                <div>Quasar v{{ $q.version }}
                
                
                
                </div>

                <q-btn
                    flat
                    dense
                    round
                    icon="menu"
                    aria-label="Menu"
                    @click="toggleRightDrawer"
                />




            </q-toolbar>
        </q-header>
<!--
        <q-drawer
            v-model="leftDrawerOpen"
            show-if-above
            bordered
        >
            <q-list>
                <q-item-label
                    header
                >
                    Favorite Websites
                </q-item-label>

                <EssentialLink
                    v-for="link in essentialLinks"
                    :key="link.title"
                    v-bind="link"
                />
            </q-list>
        </q-drawer>


-->

        <q-page-container>

                <maunzer-list heading-text="Career / Education"></maunzer-list>
                <maunzer-list heading-text="Awards"></maunzer-list>
                <maunzer-list heading-text="Skills"></maunzer-list>
                <maunzer-list heading-text="Languages"></maunzer-list>
                        

        </q-page-container>

        <q-drawer
            v-model="rightDrawerOpen"
            show-if-above
            bordered
            side="right"
        >
            <q-list>
                <q-item-label
                    header
                >
                    Favorite Websites
                </q-item-label>

                <EssentialLink
                    v-for="link in essentialLinks"
                    :key="link.title"
                    v-bind="link"
                />
            </q-list>
        </q-drawer>




    </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'

import MaunzerList from 'components/MaunzerList.vue';

const linksList = [
    {
        title: 'IntFiction.org',
        caption: 'Your place to discuss Interactive Fiction',
        icon: 'all_inbox',
        link: 'https://www.intfiction.org'
    },
    {
        title: 'Github',
        caption: 'github.com/quasarframework',
        icon: 'code',
        link: 'https://github.com/quasarframework'
    },
    {
        title: 'Discord Chat Channel',
        caption: 'chat.quasar.dev',
        icon: 'chat',
        link: 'https://chat.quasar.dev'
    },
    {
        title: 'Forum',
        caption: 'forum.quasar.dev',
        icon: 'record_voice_over',
        link: 'https://forum.quasar.dev'
    },
    {
        title: 'Twitter',
        caption: '@quasarframework',
        icon: 'rss_feed',
        link: 'https://twitter.quasar.dev'
    },
    {
        title: 'Facebook',
        caption: '@QuasarFramework',
        icon: 'public',
        link: 'https://facebook.quasar.dev'
    },
    {
        title: 'Quasar Awesome',
        caption: 'Community Quasar projects',
        icon: 'favorite',
        link: 'https://awesome.quasar.dev'
    }
]

export default defineComponent({
    name: 'MainLayout',

    components: {
        EssentialLink,
        MaunzerList,
    },

    methods: {
        nigga: function() {

        }
    },

    setup () {
        const leftDrawerOpen = ref(false)
        const rightDrawerOpen = ref(true)

        return {
            essentialLinks: linksList,
            leftDrawerOpen,
            rightDrawerOpen,
            toggleLeftDrawer () {
                leftDrawerOpen.value = !leftDrawerOpen.value
            },

            toggleRightDrawer () {
                rightDrawerOpen.value = !rightDrawerOpen.value
            },

            
        }
    }
})
</script>
