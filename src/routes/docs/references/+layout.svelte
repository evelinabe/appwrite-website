<script lang="ts" context="module">
    export function getReferencesContext() {
        return getContext<Writable<boolean>>('references-expandable');
    }
</script>

<script lang="ts">
    import { page } from '$app/stores';
    import Docs from '$lib/layouts/Docs.svelte';
    import { preferredPlatform, preferredVersion } from '$lib/utils/references';
    import { writable, type Writable } from 'svelte/store';
    import { getContext, setContext } from 'svelte';
    import Sidebar, { type NavParent, type NavTree } from '$lib/layouts/Sidebar.svelte';

    const expandable = setContext('references-expandable', writable(false));

    $: prefix = `/docs/references/${$preferredVersion ?? $page.params?.version ?? 'cloud'}/${
        $preferredPlatform ?? $page.params?.platform ?? 'client-web'
    }`;
    $: navigation = [
        {
            label: 'Getting started',
            items: [
                {
                    label: 'Overview',
                    href: '/docs/references',
                    icon: 'icon-view-grid'
                }
            ]
        },
        {
            label: 'APIs',
            items: [
                {
                    label: 'Account',
                    icon: 'icon-user',
                    href: `${prefix}/account`
                },
                {
                    label: 'Users',
                    icon: 'icon-user-group',
                    href: `${prefix}/users`
                },
                {
                    label: 'Teams',
                    icon: 'icon-users',
                    href: `${prefix}/teams`
                },
                {
                    label: 'Databases',
                    icon: 'icon-database',
                    href: `${prefix}/databases`
                },
                {
                    label: 'Storage',
                    icon: 'icon-folder',
                    href: `${prefix}/storage`
                },
                {
                    label: 'Functions',
                    icon: 'icon-lightning-bolt',
                    href: `${prefix}/functions`
                },
                {
                    label: 'Localization',
                    icon: 'icon-location-marker',
                    href: `${prefix}/locale`
                },
                {
                    label: 'Avatars',
                    icon: 'icon-user-circle',
                    href: `${prefix}/avatars`
                }
            ]
        }
        // {
        // 	label: 'Debugging',
        // 	items: [
        // 		{
        // 			icon: 'icon-document-search',
        // 			label: 'Response codes',
        // 			href: '/docs/advanced/platform/response-codes'
        // 		},
        // 		{
        // 			icon: 'icon-document-report',
        // 			label: 'Rate-limits',
        // 			href: '/docs/advanced/platform/rate-limits'
        // 		}
        // 	]
        // }
    ] as NavTree;

    const parent: NavParent = {
        href: '/docs',
        label: 'References'
    };
</script>

<Docs variant={$expandable ? 'expanded' : 'two-side-navs'} isReferences={$expandable}>
    <Sidebar {navigation} expandable={$expandable} {parent} />
    <slot />
</Docs>
