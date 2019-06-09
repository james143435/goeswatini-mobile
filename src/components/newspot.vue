<template>
    <div>
        <v-dialog
                v-model="show_dialog"
                max-width="500px"
                fullscreen
        >
        <v-card tile>
            <v-toolbar card dark prominent color="primary">
                  <v-btn icon dark @click="show_dialog = false">
            <v-icon>close</v-icon>
          </v-btn>
                <v-toolbar-title>Create A new Place Of Interest</v-toolbar-title>
                <v-spacer></v-spacer>
                <v-toolbar-items>
                    <v-btn dark flat @click.native="save_queue">Save</v-btn>
                </v-toolbar-items>
                <v-menu bottom right offset-y>
                </v-menu>
            </v-toolbar>
            <v-card-text>
                <uform :fields="general_form.fields" :title="general_form.title" :value="general_form.data" v-model="general_form.data">
                </uform>
                <slot></slot>
            </v-card-text>
        </v-card>

        </v-dialog>

    </div>

</template>

<script>
    import uform from './uform'

    export default {
        parse_class: 'queue',
        name: "newqueue",
        props: ['dialog'],
        components: {uform},
        data() {
            return {
                service: {},
                //ui
                general_form: {
                    title: 'General Information',
                    data:{},
                    fields:
                        [
                            {label: "Spot Name", v_model: 'name', type: 'text', id: 0},
                            {label: "Spot Name", v_model: 'type', type: 'select', items:['Restuarant','police station','Hotel','Museum','Polie Station'],id: 0}
                        ]
                }
            }
        },
        computed:{
          show_dialog:{
            get(){
              return this.dialog
            },
            set(dig){
              this.$emit('close')
            }

          }
        },
        created(){
            //this.get_my_service()
        },
        methods: {
            save_queue() {
                let queue = {
                    ...this.general_form.data
                }

                this.$emit('save',queue)
            }
        }

    }
</script>

<style scoped>

</style>
