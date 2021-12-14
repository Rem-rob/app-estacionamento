<template>

<div id="carro-table">

    <div>

        <div id="carro-table-heading">

            <div class="order-id" >#:</div>
            <div>Nome da pessoa</div>
            <div>Nome do carro </div>
            <div>Placa do carro</div>
            <div>Horário de entrada</div>
            <div>Ações</div>

        </div>
     </div>

    <div id="carro-table-rows">

        <div class="carro-table-row" >

            <div class="order-number">1</div>
            <div> Leo </div>
            <div> Corsa </div>
            <div> GTS-5555</div>
            <div> 08:00</div>

            <div>

                <select name="status" class="status">
                    <option value="" >Status carro</option>
                </select>

                <button class="delete-btn"> Deletar </button>

            </div>



        </div>

    </div>

</div>
    
</template>

<script>

export default {
    name: "Dashboard"
}

</script>

<style scoped>

#carro-table {
    max-width: 1200px;
    margin: 0 auto;

}

#carro-table-heading,
#carro-table-rows,
.carro-table-row {
    display: flex;
    flex-wrap: wrap;

}

#carro-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid rgba(53,30,180);
}

#carro-table-heading div,
.carro-table-row div {
    width: 19%;
}

#carro-table-rows {
    width: 100%;
    padding: 12px;
     border-bottom: 1px solid rgba(53,30,180);

}


.carro-table-row .order-number {
    width: 5%;

}

select {
    padding: 10px 6px;
    margin-right: 12px;
}

</style>