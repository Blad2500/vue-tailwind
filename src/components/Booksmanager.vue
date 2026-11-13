<script setup>
import { getBooks } from '../api/books';
</script> 

<script>
export default{
    name: "Booksmanager",
    data(){
        return {
            books: [],

        }
    },
    methods: {
        async loadbooks() {
            this.books = await getBooks();
        },
    },
    mounted(){
        this.loadbooks();
    },
};
</script>

<template>
    <main class="flex justify-center items-center flex-col">
        <h1 class="">
            Könyvtár kezelő felület
        </h1>

        <table class="">
            <thead class="">
                <tr class="">
                    <th class="">Azonosito</th>
                    <th class="">Cim</th>
                    <th class="">Szerzo</th>
                    <th class="">Megjelenes ev</th>
                    <th class="">Muveletek</th>
                </tr>
            </thead>
            <tbody class="">
                <tr v-for="book in books" :key="book.id" class="">
                    <td class="">{{ book.id }}</td>
                    <td class="">{{ book.title }}</td>
                    <td class="">{{ book.author }}</td>
                    <td class="">{{ book.year }}</td>
                    <td class="">-</td>
                </tr>
            </tbody>
        </table>
    </main> 
</template>