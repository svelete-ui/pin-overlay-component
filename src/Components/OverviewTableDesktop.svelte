<script>
    import { pad } from "../lib/datetime.js";

    let today = new Date();
    var date =
        today.getFullYear() +
        "\t" +
        pad(today.getDate(), 2) +
        "." +
        pad(today.getMonth() + 1, 2);

    let putzplan = {
        id: "11004422",
        members: ["David", "Jonas", "Leoni", "Maria", "Yara"],
        dueDates: ["31.07", "07.08", "14.08"],
    };

// {
// id: "11004422"
// date: "31.07.2022"
// Rooms [    
    // kitchen {
        // Status - null?/open, done, wontdo
        // 
        // }
    // ]
    // 
// 

</script>

<!-- <h2>{date}</h2> -->
<!-- https://stackoverflow.com/questions/2259189/table-overflowing-outside-of-div -->
<table class="putz-table">
    <tr>
        <th class="table-padding date-width">datum</th>
        <!-- <th class="table-padding" /> -->
        <th class="table-padding entry-width">küche</th>
        <th class="table-padding entry-width">flur</th>
        <th class="table-padding entry-width">müll</th>
        <th class="table-padding entry-width">bad</th>
        <th class="table-padding entry-width">chillen</th>
    </tr>
    {#each [...putzplan.dueDates] as dueDate, dateIndex}
        <tr>
            <td class="table-padding done-td-bg">{dueDate}</td>
            <!-- <td class="table-padding invisible-td-bg" /> -->
            {#each [...putzplan.members] as member, memberIndex}
                <td class="table-padding done-td-bg">
                    {putzplan.members[
                        (memberIndex + dateIndex) % putzplan.members.length
                    ]}
                </td>
            {/each}
        </tr>
    {/each}
</table>

<style>

.date-width{
    width: 35px;
}
.entry-width{
    width: 50px;
}
    .undone-td-bg {
        background-color: #fdae65d8;
    }

    .done-td-bg {
        background-color: #40d371c4;
    }

    .header-td-bg {
        background-color: #63d3c657;
        color: #2a9d8f;
    }

    .putz-table {
        border-collapse: inherit;
        border-spacing: 10px;
        /* table-layout: fixed; */
        /* width: auto; */
        width:100%;
        table-layout: fixed; 

    }

    .table-padding {
        padding-top: 5px;
        padding-bottom: 5px;
        padding-left: 10px;
        padding-right: 10px;
    }
    * {
        font-family: "Raleway", sans-serif;
    }
</style>
