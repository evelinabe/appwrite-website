<script context="module" lang="ts">
    export type AuthorData = {
        name: string;
        slug: string;
        role: string;
        avatar: string;
        bio: string;
        twitter: string;
        linkedin: string;
        github: string;
        href: string;
    };
</script>

<script lang="ts">
    import { Article, FooterNav, MainFooter } from '$lib/components';
    import { page } from '$app/stores';
    import { Main } from '$lib/layouts';
    import { getContext } from 'svelte';
    import type { PostsData } from './Post.svelte';
    import { BLOG_TITLE_SUFFIX } from '$routes/titles';
    import { DEFAULT_HOST } from '$lib/utils/metadata';
    import FloatingHead from '$lib/components/FloatingHead.svelte';

    export let name: string;
    export let role: string;
    export let avatar: string;
    export let bio: string;
    export let twitter: string;
    export let linkedin: string;
    export let github: string;

    const posts = getContext<PostsData[]>('posts');
    const authors = getContext<AuthorData[]>('authors');
    const author = authors.find(
        (p) => $page.url.pathname.substring($page.url.pathname.lastIndexOf('/') + 1) === p.slug
    );

    const seoTitle = name + BLOG_TITLE_SUFFIX;
    const description = bio;
    const ogImage = DEFAULT_HOST + '/images/open-graph/blog.png';
</script>

<svelte:head>
    <!-- Titles -->
    <title>{seoTitle}</title>
    <meta property="og:title" content={seoTitle} />
    <meta name="twitter:title" content={seoTitle} />
    <!-- Desscription -->
    <meta name="description" content={description} />
    <meta property="og:description" content={description} />
    <meta name="twitter:description" content={description} />
    <!-- Image -->
    <meta property="og:image" content={ogImage} />
    <meta property="og:image:width" content="1200" />
    <meta property="og:image:height" content="630" />
    <meta name="twitter:image" content={ogImage} />
    <meta name="twitter:card" content="summary_large_image" />
</svelte:head>

<Main>
    <div class="aw-big-padding-section-level-1 u-position-relative u-overflow-hidden">
        <div
            class="u-position-absolute"
            style="pointer-events:none;inset-inline-start:0; inset-block-end:0;"
        >
            <svg
                xmlns="http://www.w3.org/2000/svg"
                width="660"
                height="497"
                viewBox="0 0 660 497"
                fill="none"
            >
                <g opacity="0.4" filter="url(#filter0_f_2092_11792)">
                    <ellipse
                        cx="-2.5"
                        cy="609.5"
                        rx="362.5"
                        ry="309.5"
                        fill="url(#paint0_radial_2092_11792)"
                    />
                </g>
                <defs>
                    <filter
                        id="filter0_f_2092_11792"
                        x="-665"
                        y="0"
                        width="1325"
                        height="1219"
                        filterUnits="userSpaceOnUse"
                        color-interpolation-filters="sRGB"
                    >
                        <feFlood flood-opacity="0" result="BackgroundImageFix" />
                        <feBlend
                            mode="normal"
                            in="SourceGraphic"
                            in2="BackgroundImageFix"
                            result="shape"
                        />
                        <feGaussianBlur
                            stdDeviation="150"
                            result="effect1_foregroundBlur_2092_11792"
                        />
                    </filter>
                    <radialGradient
                        id="paint0_radial_2092_11792"
                        cx="0"
                        cy="0"
                        r="1"
                        gradientUnits="userSpaceOnUse"
                        gradientTransform="translate(-2.5 629.739) rotate(90) scale(289.261 362.5)"
                    >
                        <stop offset="0.281696" stop-color="#FE9567" />
                        <stop offset="0.59375" stop-color="#FD366E" />
                    </radialGradient>
                </defs>
            </svg>
        </div>

        <div class="aw-big-padding-section-level-2 u-position-relative">
            <div class="aw-container">
                <div class="aw-author-section u-block">
                    {#if avatar}
                        <FloatingHead --position="relative" src={avatar} alt={name} size={112} />
                    {/if}
                    <h1 class="aw-title aw-u-color-text-primary">{name}</h1>
                    {#if role}
                        <div class="aw-label u-margin-block-start-8">{role}</div>
                    {/if}
                    {#if bio}
                        <p class="aw-author-section-info aw-description">
                            {bio}
                        </p>
                    {/if}
                    <ul class="u-flex u-main-center u-gap-8">
                        {#if github}
                            <li>
                                <a
                                    href={github}
                                    class="aw-icon-button"
                                    aria-label="Author GitHub"
                                    target="_blank"
                                    rel="noopener noreferrer"
                                >
                                    <span class="aw-icon-github" aria-hidden="true" />
                                </a>
                            </li>
                        {/if}
                        {#if twitter}
                            <li>
                                <a
                                    href={twitter}
                                    class="aw-icon-button"
                                    aria-label="Author twitter"
                                    target="_blank"
                                    rel="noopener noreferrer"
                                >
                                    <span class="aw-icon-x" aria-hidden="true" />
                                </a>
                            </li>
                        {/if}
                        {#if linkedin}
                            <li>
                                <a
                                    href={linkedin}
                                    class="aw-icon-button"
                                    aria-label="Author LinkedIn"
                                    target="_blank"
                                    rel="noopener noreferrer"
                                >
                                    <span class="aw-icon-linkedin" aria-hidden="true" />
                                </a>
                            </li>
                        {/if}
                    </ul>
                </div>
            </div>
        </div>
    </div>

    <div class="aw-big-padding-section-level-1">
        <div class="aw-big-padding-section-level-2">
            <div class="aw-container">
                <h2 class="aw-title aw-u-color-text-primary">Articles</h2>

                <!-- <div class="aw-is-only-mobile u-margin-block-start-32">
					<label class="u-block aw-select is-colored" for="articles">
						<select id="articles">
							<option>Latest</option>
							<option>News</option>
							<option>Insights</option>
							<option>Tutorials</option>
							<option>Changelog</option>
						</select>
						<span class="icon-cheveron-down" aria-hidden="true" />
					</label>
				</div> -->
                <!--<div class="aw-is-not-mobile">
					<div class="u-flex u-main-space-between u-gap-16 u-margin-block-start-24">
						<ul
							class="aw-secondary-tabs is-transparent"
							role="tablist"
							aria-orientation="horizontal"
							data-orientation="horizontal"
							data-melt-tabs-list=""
						>
							<li class="aw-secondary-tabs-item">
								<button
									class="aw-secondary-tabs-button u-width-full-line is-selected"
									type="button"
									role="tab"
									data-state="active"
									tabindex="0"
									data-value="Cloud"
									data-orientation="horizontal"
									data-melt-tabs-trigger=""
								>
									<span class="aw-main-body-500">Latest</span>
								</button>
							</li>
							<li class="aw-secondary-tabs-item">
								<button
									class="aw-secondary-tabs-button u-width-full-line"
									type="button"
									role="tab"
									data-state="inactive"
									tabindex="-1"
									data-value="Self-Hosted"
									data-orientation="horizontal"
									data-melt-tabs-trigger=""
								>
									<span class="aw-main-body-500">News</span>
								</button>
							</li>
							<li class="aw-secondary-tabs-item">
								<button
									class="aw-secondary-tabs-button u-width-full-line"
									type="button"
									role="tab"
									data-state="inactive"
									tabindex="-1"
									data-value="Self-Hosted"
									data-orientation="horizontal"
									data-melt-tabs-trigger=""
								>
									<span class="aw-main-body-500">Insights</span>
								</button>
							</li>
							<li class="aw-secondary-tabs-item">
								<button
									class="aw-secondary-tabs-button u-width-full-line"
									type="button"
									role="tab"
									data-state="inactive"
									tabindex="-1"
									data-value="Self-Hosted"
									data-orientation="horizontal"
									data-melt-tabs-trigger=""
								>
									<span class="aw-main-body-500">Tutorials</span>
								</button>
							</li>
							<li class="aw-secondary-tabs-item">
								<button
									class="aw-secondary-tabs-button u-width-full-line"
									type="button"
									role="tab"
									data-state="inactive"
									tabindex="-1"
									data-value="Self-Hosted"
									data-orientation="horizontal"
									data-melt-tabs-trigger=""
								>
									<span class="aw-main-body-500">Changelog</span>
								</button>
							</li>
						</ul> -->
                <!-- <div class="aw-input-text-search-wrapper">
							<span class="icon-search" aria-hidden="true" />
							<input class="aw-input-text aw-u-block-size-48" type="search" placeholder="Search" />
						</div> 
					</div>
				</div>-->

                <div class="u-margin-block-start-48">
                    <ul class="aw-grid-articles">
                        {#each posts.filter((p) => p.author === author?.slug) as post}
                            <Article
                                title={post.title}
                                href={post.href}
                                cover={post.cover}
                                date={post.date}
                                timeToRead={post.timeToRead}
                                {avatar}
                                author={name}
                            />
                        {/each}
                    </ul>
                </div>
            </div>
        </div>
        <div
            class="aw-big-padding-section-level-2 is-margin-replace-padding u-position-relative u-overflow-hidden"
        >
            <div class="aw-container">
                <FooterNav />
                <MainFooter />
            </div>
        </div>
    </div>
</Main>
