<template>
    <div>
        <div class="header bg-primary pb-6">
            <div class="container-fluid">
                <div class="header-body">
                    <div class="row align-items-center py-4">
                        <div class="col-lg-6 col-7">
                            <h6 class="h2 text-white d-inline-block mb-0">Setting</h6>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="container-fluid mt--6">
            <div class="row">
                <div class="col-xl-8 order-xl-1">
                    <div class="card">
                        <div class="card-body">
                            <form>
                                <h6 class="heading-small text-muted mb-4">Change Password</h6>
                                <ChangePassword></ChangePassword>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>

<script>

import ChangePassword from "./ChangePassword";
export default {
    name: "Setting",
    components: {ChangePassword},
    data(){
        return{}
    }
}
</script>
