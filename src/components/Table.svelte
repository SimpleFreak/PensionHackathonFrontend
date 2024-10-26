<script>
// @ts-nocheck

    export let users
</script>

<!-- <div class="_table-container">
    <table class="table">
        <thead>
            <tr>
                {#each Object.keys(users[0]) as columnHeading}
                    <th>{columnHeading}</th>
                {/each}
            </tr>
        </thead>
        <tbody>
            {#each Object.values(users) as row}
                <tr>
                    {#each Object.values(row) as cell}
                        <td>{cell}</td>
                    {/each}
                </tr>
            {/each}
        </tbody>
    </table>
</div> -->

<style>
._table-container{
    margin: 20px 0px;
}
.table {

width: 100%;

border: none;

margin-bottom: 20px;

}

.table thead th {

font-weight: bold;

text-align: left;

border: none;

padding: 10px 15px;

background: #275e0e;
color: #f3f3f3;
font-size: 14px;

}

.table thead tr th:first-child {

border-radius: 8px 0 0 8px;

}

.table thead tr th:last-child {

border-radius: 0 8px 8px 0;

}

.table tbody td {

    text-align: left;

    border: none;

    padding: 10px 15px;

    font-size: 14px;

    vertical-align: top;

}

.table tbody tr:nth-child(even){

    background: #f3f3f3;

}

.table tbody tr td:first-child {

    border-radius: 8px 0 0 8px;

}

.table tbody tr td:last-child {

border-radius: 0 8px 8px 0;

}
</style>