<template>
    <div>
        Сьоме завдання
        <br>
        <label for="rows">Кількість рядків:</label>
        <input v-model="rowCount" type="number" min="1" @input="createTable" />
        <br />
        <label for="columns">Кількість стовпців:</label>
        <input v-model="columnCount" type="number" min="1" @input="createTable" />
        <br />
        <table>
            <tr v-for="(row, rowIndex) in tableData" :key="rowIndex">
                <td v-for="(col, colIndex) in row" :key="colIndex">{{ col }}</td>
            </tr>
        </table>
    </div>
</template>

<script>
export default {
    data() {
        return {
            rowCount: 1,
            columnCount: 1,
            tableData: []
        };
    },
    methods: {
        createTable() {
            this.tableData = [];
            for (let i = 0; i < this.rowCount; i++) {
                let tmp = [];
                for (let j = 0; j < this.columnCount; j++) {
                    tmp.push(`|Рядок ${i + 1}: Стовпець ${j + 1}|`)
                }
                this.tableData.push(tmp);
            }
        }
    },
}
</script>
