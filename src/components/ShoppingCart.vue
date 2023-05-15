<script>
import { computed } from '@vue/reactivity';
import { toHandlers } from 'vue';

export default {
    data(){
        return {
            adultPrice: 6.99,
            childPrice: 3.99
        }
    },
    props: {
        adultCountObj: {
            type: Object,
            default: {
                
            }
        },
        childCountObj: {
            type: Object,
            default: {
                
            }
        }
    },
    methods: {
        decrementTicket(obj, key)
        {
            obj[key]--;
            this.$emit("updateCount", this.adultCountObj, this.childCountObj);
        },
        incrementTicket(obj, key)
        {
            obj[key]++;
            this.$emit("updateCount", this.adultCountObj, this.childCountObj);
        },
        deleteTicket(obj, key)
        {
            obj[key] = 0;
            this.$emit("updateCount", this.adultCountObj, this.childCountObj);
        },
    },
    computed: {
        totalAdultPrice()
        {
            var totalPrice = 0;
            Object.values(this.adultCountObj).forEach(value => {
                totalPrice += (value * 6.99);
            })
            return totalPrice;
        },
        totalChildPrice()
        {
            var totalPrice = 0;
            Object.values(this.childCountObj).forEach(value => {
                totalPrice += (value * 3.99);
            })
            return totalPrice;
        },
        totalPrice(){
            return this.totalAdultPrice + this.totalChildPrice;
        },
        totalTickets()
        {
            var tickets = 0;
            Object.values(this.adultCountObj).forEach(value => {
                tickets += value;
            });
            Object.values(this.childCountObj).forEach(value => {
                tickets += value;
            })
            return tickets;
        }
    }
}
</script>

<template>
    <aside>
        <h2>Adult Tickets</h2>
        <hr>
        <table>
            <tbody v-for="(item, key) in adultCountObj">
                <tr v-if="item > 0">
                    <td><a class="delete" @click="deleteTicket(this.adultCountObj, key)">X</a></td>
                    <td>{{ key }}</td>
                    <td> {{ item }} / Tickets</td>
                    <td> {{ "$" + (item * adultPrice) }}</td>
                    <td><button class="btn btn-danger" @click="decrementTicket(adultCountObj, key)">-</button></td>
                    <td><button class="btn btn-primary" @click="incrementTicket(adultCountObj, key)">+</button></td>
                </tr>
            </tbody>
            <tfoot>
                <tr>
                    <td colspan="4">Total Adult Price</td>
                    <td></td>
                    <td>${{ totalAdultPrice }}</td>
                </tr>
            </tfoot>
        </table>
        <h2>Child Tickets</h2>
        <hr>
        <table>
            <tbody v-for="(item, key) in childCountObj">
                <tr v-if="item > 0">
                    <td><a class="delete" @click="deleteTicket(this.childCountObj, key)">X</a></td>
                    <td>{{ key }}</td>
                    <td>{{ item }} / Tickets</td>
                    <td> {{ "$" + (item * childPrice) }}</td>
                    <td><button class="btn btn-danger" @click="decrementTicket(childCountObj, key)">-</button></td>
                    <td><button class="btn btn-primary" @click="incrementTicket(childCountObj, key)">+</button></td>
                </tr>
            </tbody>
            <tfoot>
                <tr>
                    <td colspan="4">Total Child Price</td>
                    <td></td>
                    <td>${{ totalChildPrice }}</td>
                </tr>
            </tfoot>
        </table>
        <h2>Totals</h2>
        <hr>
        <table>
            <tr><td>Total Tickets: </td><td></td><td>{{ totalTickets }}</td></tr>
            <tr><td>Total Price: </td><td></td><td>${{ totalPrice }}</td></tr>
        </table>
    </aside>
</template>

<style scoped>
    aside {
        padding: 1rem;
        margin: 0.5rem;
        border-radius: 35px;
        background-color: var(--color-border);
    }
    td {
        padding: 0.75rem;
    }

    .delete{
        padding: 0.2rem;
        border-radius: 40px;
        color: red;
        text-decoration: none;
    }
    .delete:hover {
        cursor:pointer;
        background-color: var(--color-background);
    }
    .btn {
        text-align: center;
        padding: 0px;
        margin: 0.25rem;
        width: 30px;
        height: 30px;
        border-radius: 50%;
        font-size: 1.5rem;
    }

    h2 {
        margin-top: 1rem;
    }
</style>