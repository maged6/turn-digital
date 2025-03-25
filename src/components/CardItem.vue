<template>
    <div class="card-item">
        <div class="card-item-img">
            <img :src="dataItem.img" alt="" />
        </div>
        <div class="card-item-content">
            <h3 class="capitalize-text start-text">{{ dataItem.name }}</h3>
            <p> {{  dataItem.sub_title }}</p>
            <span class="start-text"> <strong> {{  dataItem.price }}</strong></span>
            <div class="card-item-quantity">
                <label for="quantity">Quantity</label>
                <select >
                   <option value="" class="input-select">1</option>
                   <option value="" class="input-select">2</option>
                   <option value="" class="input-select">3</option>
                </select>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'CardItem',
    props: {
        dataItem: Object,
        default: () => {}
    }
}
</script>