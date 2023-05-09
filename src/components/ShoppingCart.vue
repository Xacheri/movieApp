<template>
    <aside>
        <table>
            <tr v-for="movie in movies">
                <td><a>X</a></td><th>{{ movie.original_title }}</th><td>{{ adultCount }} Adult Tickets [{{ adultCost }}]</td><td>{{ childCount }} Child Tickets [{{ childCost }}]</td>
            </tr>
        </table>
    </aside>
</template>

<script>
export default {
    data(){

    },
    props: [movies, adultCount, childCount]
}
</script>