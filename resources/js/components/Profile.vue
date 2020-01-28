<style scoped>
    .widget-user-header {
        background-position: center center;
        background-size: cover;
        height: 250px !important;
    }
</style>
<template>
    <div class="container">
        <div class="row">
            <div class="col-md-12 mt-3">
                <div class="card card-widget widget-user">
                    <!-- Add the bg color to the header using any of the bg-* classes -->
                    <div class="widget-user-header text-white"
                         style="background: url('./img/user_cover.png') center center;">
                        <h3 class="widget-user-username text-right">Elizabeth Pierce</h3>
                        <h5 class="widget-user-desc text-right">Web Designer</h5>
                    </div>
                    <div class="widget-user-image">
                        <img class="img-circle" src="" alt="User Avatar">
                    </div>
                    <div class="card-footer">
                        <div class="row">
                            <div class="col-sm-4 border-right">
                                <div class="description-block">
                                    <h5 class="description-header">3,200</h5>
                                    <span class="description-text">SALES</span>
                                </div>
                                <!-- /.description-block -->
                            </div>
                            <!-- /.col -->
                            <div class="col-sm-4 border-right">
                                <div class="description-block">
                                    <h5 class="description-header">13,000</h5>
                                    <span class="description-text">FOLLOWERS</span>
                                </div>
                                <!-- /.description-block -->
                            </div>
                            <!-- /.col -->
                            <div class="col-sm-4">
                                <div class="description-block">
                                    <h5 class="description-header">35</h5>
                                    <span class="description-text">PRODUCTS</span>
                                </div>
                                <!-- /.description-block -->
                            </div>
                            <!-- /.col -->
                        </div>
                        <!-- /.row -->
                    </div>
                </div>
            </div>
            <div class="col-md-12">
                <div class="card">
                    <div class="card-header p-2">
                        <ul class="nav nav-pills">
                            <li class="nav-item active"><a class="nav-link active" href="#activity" data-toggle="tab">Activity</a>
                            </li>

                            <li class="nav-item"><a class="nav-link " href="#settings" data-toggle="tab">Settings</a>
                            </li>
                        </ul>
                    </div><!-- /.card-header -->
                    <div class="card-body">
                        <div class="tab-content">
                            <div class="tab-pane text-center" id="activity">
                                <h1>Display User Activity</h1>
                            </div>

                            <!-- /.tab-pane -->

                            <div class="tab-pane" id="settings">
                                <form class="form-horizontal">
                                    <div class="form-group">
                                        <label for="name" class="col-sm-12 col-form-label">Name</label>
                                        <div class="col-sm-12">
                                            <input v-model="form.name" type="text" name="name" class="form-control" id="name" placeholder="Name">
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="email" class="col-sm-12 col-form-label">Email</label>
                                        <div class="col-sm-12">
                                            <input v-model="form.email" type="email" name="email" class="form-control" id="email"
                                                   placeholder="Email">
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="bio" class="col-sm-12 col-form-label">Experience</label>
                                        <div class="col-sm-12">
                                            <textarea v-model="form.bio" class="form-control" name="bio" id="bio"
                                                      placeholder="Experience"></textarea>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="photo" class="col-sm-12 col-form-label">Profile Photo</label>
                                        <div class="col-sm-12">
                                            <input type="file" @change="updateProfile" name="photo" class="form-control" id="photo">
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="passport" class="col-sm-12 col-form-label">Passport(leave empty if not changing)</label>
                                        <div class="col-sm-12">
                                            <input type="text" class="form-control" name="passport" id="passport" placeholder="Passport">
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <div class="col-sm-2">
                                            <button @click.prevent="updateInfo" type="submit" class="btn btn-success">Update</button>
                                        </div>
                                    </div>
                                </form>
                            </div>
                            <!-- /.tab-pane -->
                        </div>
                        <!-- /.tab-content -->
                    </div><!-- /.card-body -->
                </div>
                <!-- /.nav-tabs-custom -->
            </div>
        </div>
    </div>
</template>


<script>
    export default {
        data(){
            return {
                form: new Form({
                    id: '',
                    name: '',
                    email: '',
                    password: '',
                    type: '',
                    bio: '',
                    photo: '',
                })
            }
        },
        name: "Profile",
        methods:{
            updateInfo(){
                this.form.put('api/profile/')
                    .then(()=>{

                    })
                    .catch(()=>{

                    });
            },
           updateProfile(e){
               //console.log('uploading')
               let file = e.target.files[0];
               // console.log(file);
               let reader = new FileReader();
               reader.onloadend = (file) => {
                  // console.log('RESULT', reader.result)
                   this.form.photo = reader.result
               }

               reader.readAsDataURL(file);
           }
        },

        created() {
            axios.get("api/profile")
                .then(({data})=> (this.form.fill(data)));
        }
    }
</script>


