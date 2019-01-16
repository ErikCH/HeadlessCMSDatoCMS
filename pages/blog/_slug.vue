<template>
    <div>
        <h1 v-if="post"> {{ post.title }}</h1>
        <h1 v-if="post"> {{ post.body }}</h1>
    </div>
</template>


<script>

import gql from 'graphql-tag';
export default {

    apollo: {
        post: {
            query: gql`query Post($slug: String!){
                post(filter: { slug: {
                    matches: { pattern: $slug }

                }}) {
                    title
                    body
                    
                }
            }`,
            prefetch({route}) {
                return {
                    slug: route.params.slug
                }
            },
            variables() {
                return {
                    slug: this.$route.params.slug
                }
            }
        }
    }

}
</script>
