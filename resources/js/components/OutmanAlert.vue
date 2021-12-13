<template>
    <div class="container" v-if="alerting">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="alert alert-danger" role="alert">
                    您的账号已在别处登录！
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: [
        'id'
    ],
    data() {
        return {
            alerting: false
        }
    },
    mounted() {
        window.Echo.channel('outman-user-' + this.id).listen('UserAuthenticatedEvent', () => {
            this.alerting = true
            setTimeout(() => {
                window.location = '/login'
            }, 3000)
        })
    }
}
</script>
