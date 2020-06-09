<template>
    <article class="page">
        <h1>{{title}}</h1>
        <aside>
            <slot name="aside"></slot>
        </aside>
        <section>
            <slot></slot>
        </section>
    </article>
</template>

<script>
export default {
    name: 'page',
    props: {
        title: String
    }
}
</script>

<style lang="sass" scoped>
    @import "@/sass/main.sass";
    .page
        & > *
            overflow: hidden
            padding: $padding

        h1
            width: 100%
            text-align: center
            border-bottom: $border
            margin-bottom: $margin

        aside
            float: left
            width: 250px
            @include position(sticky, $nav-height, 0)

            h6
                padding: $padding/2 0
        
        section
            padding: 0 $padding/2
            border-left: $border
            min-height: 400px
</style>