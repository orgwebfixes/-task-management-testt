<template>
    <div class="col-xl-8 order-xl-1">
        <div class="card">
            <div class="card-header">
                <div class="row align-items-center">
                    <div class="col-8">
                        <h3 class="mb-0">Edit profile </h3>
                    </div>
                    <div class="col-4 text-right">
                        <button class="btn btn-sm btn-primary" v-on:click="updateProfile()">Update Profile</button>
                    </div>
                </div>
            </div>
            <div class="card-body" id="myProfileLoading">
                <form>
                    <h6 class="heading-small text-muted mb-4">User information</h6>
                    <div class="pl-lg-4">
                        <div class="row">
                            <div class="col-lg-6">
                                <div class="form-group">
                                    <label class="form-control-label" for="input-email">Email Id</label>
                                    <input type="text" id="input-email" class=" form-control-plaintext" readonly v-model="profile.email">
                                </div>
                            </div>
                            <div class="col-lg-6">
                                <div class="form-group">
                                    <label class="form-control-label" for="input-username">Username</label>
                                    <input type="text" id="input-username" class="form-control" placeholder="Username" v-model="profile.name">
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-lg-6">
                                <div class="form-group">
                                    <label class="form-control-label" for="input-first-name">First name</label>
                                    <input type="text" id="input-first-name" class="form-control" placeholder="First name" v-model="profile.first_name">
                                </div>
                            </div>
                            <div class="col-lg-6">
                                <div class="form-group">
                                    <label class="form-control-label" for="input-last-name">Last name</label>
                                    <input type="text" id="input-last-name" class="form-control" placeholder="Last name" v-model="profile.last_name">
                                </div>
                            </div>
                        </div>
                    </div>
                  

                </form>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "ProfileUpdate",
    data() {
        return {
            profile: {
                name: null,
                first_name: null,
                last_name: null,
                about_me: null,
                email: null,
                phone_number: null,
                headline: null,
                address: null,
                city: null,
                country: null,
                postal_code: null,
            },
            profile_baseURL : 'assets/img/profile/',
        }
    },
    methods: {
        getProfile() {
            let Loading = this.block("myProfileLoading")
            this.axios.get("/api/v1/profile")
                .then(response => {
                    let data  = response.data.data;
                    this.profile.name = data.name;
                    this.profile.first_name = data.first_name;
                    this.profile.last_name = data.last_name;
                    this.profile.about_me = data.about_me;
                    this.profile.email = data.email;
                    this.profile.phone_number = data.phone_number;
                    this.profile.headline = data.headline;
                    this.profile.address = data.address;
                    this.profile.city = data.city;
                    this.profile.postal_code = data.postal_code;
                    this.profile.country = data.country;
                    this.profile.profile_pic = data.profile_pic;
                    Loading.close()
                })
                .catch(error => {
                    console.log(error.response.data)
                    Loading.close()
                })
        },
        updateProfile(){
            let Loading = this.block("myProfileLoading")
            this.axios.put('/api/v1/update/profile',this.profile)
                .then(response => {
                    if (response.data.status === true){
                        this.successNotification(response.data.message)
                        Loading.close();
                        this.$root.$refs.ProfileView.getProfile();
                    }else {
                        Loading.close();
                    }
                })
                .catch(error => {
                    Loading.close();
                    this.errorNotification(error.response.data.message)
                });
        }
    },
    mounted() {
        this.getProfile();
    }
}
</script>

<style scoped>

</style>
