<script>
import { computed } from '@vue/reactivity';
import { toHandlers } from 'vue';

export default {
    data(){
        return {
            adultPrice: 6.99, // price for an adult ticket
            childPrice: 3.99 // price for a child ticket
        }
    },
    props: {
        adultCountObj: 
        // take the adult count-tracking object as a prop
        {
            type: Object,
            default: {
                
            }
        },
        childCountObj:
        // take the child count-tracking object as a prop
        {
            type: Object,
            default: {
                
            }
        }
    },
    methods: {
        decrementTicket(obj, key)
        // decrement the objects value at the key in the component (countObj, moviename) send an event up the chain with both new objects
        {
            obj[key]--;
            this.$emit("updateCount", this.adultCountObj, this.childCountObj);
        },
        incrementTicket(obj, key)
        // increment the objects value at the key in the component (countObj, moviename) send an event up the chain with both new objects
        {
            obj[key]++;
            this.$emit("updateCount", this.adultCountObj, this.childCountObj);
        },
        deleteTicket(obj, key)
        // set the objects value at the key in the component (countObj, moviename) to zero send an event up the chain with both new objects
        {
            obj[key] = 0;
            this.$emit("updateCount", this.adultCountObj, this.childCountObj);
        },
    },
    computed:
    // these computed values are derived from our props to make total prices available
    {
        totalAdultPrice()
        {
            var totalPrice = 0;

            // loop through all the objects value, multiplying for price and adding to the sum
            Object.values(this.adultCountObj).forEach(value => {
                totalPrice += (value * 6.99);
            })
            return totalPrice;
        },
        totalChildPrice()
        {
            var totalPrice = 0;

            // loop through all the objects value, multiplying for price and adding to the sum
            Object.values(this.childCountObj).forEach(value => {
                totalPrice += (value * 3.99);
            })
            return totalPrice;
        },
        totalPrice(){
            // add the total prices together
            return this.totalAdultPrice + this.totalChildPrice;
        },
        totalTickets()
        // loop through all of both objects values and adding to the sum
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
            <!-- v-for can loop through objects and even provide a key as a second parameter -->
            <tbody v-for="(item, key) in adultCountObj">
                <!-- dont render if the count is 0 or less -->
                <tr v-if="item > 0">
                    <!-- On click, delete these tickets -->
                    <td><a class="delete" @click="deleteTicket(this.adultCountObj, key)">X</a></td>
                    <td>{{ key }}</td>
                    <td> {{ item }} / Tickets</td>
                    <td> {{ "$" + (item * adultPrice) }}</td>
                    <!-- On click, decrement these tickets-->
                    <td><button class="btn btn-danger" @click="decrementTicket(adultCountObj, key)">-</button></td>
                    <!-- On click, increment these tickets-->
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
            <!-- v-for can loop through objects and even provide a key as a second parameter -->
            <tbody v-for="(item, key) in childCountObj">
                <!-- dont render if the count is 0 or less -->
                <tr v-if="item > 0">
                    <!-- On click, delete these tickets -->
                    <td><a class="delete" @click="deleteTicket(this.childCountObj, key)">X</a></td>
                    <td>{{ key }}</td>
                    <td>{{ item }} / Tickets</td>
                    <td> {{ "$" + (item * childPrice) }}</td>
                    <!-- On click, decrement these tickets-->
                    <td><button class="btn btn-danger" @click="decrementTicket(childCountObj, key)">-</button></td>
                    <!-- On click, increment these tickets-->
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