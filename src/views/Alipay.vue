<template>
    <div class="alipay">
        <loading v-if="loading"></loading>
        <div class="form" v-html="content"></div>
    </div>
</template>

<script>
import Loading from "./../components/Loading";
export default {
    name: "Alipay",
    data() {
        return {
            orderId: this.$route.query.orderId,
            content: "",
            loading: true
        };
    },
    created() {
        this.paySubmit();
    },
    methods: {
        paySubmit() {
            this.$axios
                .post("/pay", {
                    orderId: this.orderId,
                    orderName: "Vue高仿小米商城",
                    amount: 0.01, //单位元
                    payType: 1 //1支付宝，2微信
                })
                .then(res => {
                    this.content = res.content;
                    setTimeout(() => {
                        // 把支付宝返回的HTML片段，是个form表单，提交了
                        document.forms[0].submit();
                        this.loading = false;
                    }, 100);
                });
        }
    },
    components: {
        Loading
    }
};
</script>
<style lang="scss" scoped></style>
