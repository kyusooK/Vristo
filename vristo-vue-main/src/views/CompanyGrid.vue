<template>
    <div style="max-height:80vh;">
        <!-- Recent Transactions -->
        <div class="panel">
            <div class="gs-bundle-of-buttons" style="max-height:10vh;">
                <v-btn @click="addNewRow" class="contrast-primary-text" small color="primary">
                    <v-icon small>mdi-plus-circle-outline</v-icon>등록
                </v-btn>
                <v-btn  @click="editSelectedRow" class="contrast-primary-text" small color="primary" >
                    <v-icon small>mdi-pencil</v-icon>수정
                </v-btn>
                <v-btn @click="deleteSelectedRows" class="contrast-primary-text" small color="primary">
                    <v-icon small>mdi-minus-circle-outline</v-icon>삭제
                </v-btn>
            </div>
            <div class="mb-5 text-lg font-bold">Recent Transactions</div>
            <div class="table-responsive">
                <table>
                    <thead>
                        <tr>
                            <th class="ltr:rounded-l-md rtl:rounded-r-md">ID</th>
                            <th>{{ value.name }}</th>
                            <th>NAME</th>
                            <th>AMOUNT</th>
                            <th class="text-center ltr:rounded-r-md rtl:rounded-l-md">STATUS</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td class="font-semibold">#01</td>
                            <td class="whitespace-nowrap">Oct 08, 2021</td>
                            <td class="whitespace-nowrap">Eric Page</td>
                            <td>$1,358.75</td>
                            <td class="text-center">
                                <span class="badge bg-success/20 text-success rounded-full hover:top-0">Completed</span>
                            </td>
                        </tr>
                        <tr>
                            <td class="font-semibold">#02</td>
                            <td class="whitespace-nowrap">Dec 18, 2021</td>
                            <td class="whitespace-nowrap">Nita Parr</td>
                            <td>-$1,042.82</td>
                            <td class="text-center">
                                <span class="badge bg-info/20 text-info rounded-full hover:top-0">In Process</span>
                            </td>
                        </tr>
                        <tr>
                            <td class="font-semibold">#03</td>
                            <td class="whitespace-nowrap">Dec 25, 2021</td>
                            <td class="whitespace-nowrap">Carl Bell</td>
                            <td>$1,828.16</td>
                            <td class="text-center">
                                <span class="badge bg-danger/20 text-danger rounded-full hover:top-0">Pending</span>
                            </td>
                        </tr>
                        <tr>
                            <td class="font-semibold">#04</td>
                            <td class="whitespace-nowrap">Nov 29, 2021</td>
                            <td class="whitespace-nowrap">Dan Hart</td>
                            <td>$1,647.55</td>
                            <td class="text-center">
                                <span class="badge bg-success/20 text-success rounded-full hover:top-0">Completed</span>
                            </td>
                        </tr>
                        <tr>
                            <td class="font-semibold">#05</td>
                            <td class="whitespace-nowrap">Nov 24, 2021</td>
                            <td class="whitespace-nowrap">Jake Ross</td>
                            <td>$927.43</td>
                            <td class="text-center">
                                <span class="badge bg-success/20 text-success rounded-full hover:top-0">Completed</span>
                            </td>
                        </tr>
                        <tr>
                            <td class="font-semibold">#06</td>
                            <td class="whitespace-nowrap">Jan 26, 2022</td>
                            <td class="whitespace-nowrap">Anna Bell</td>
                            <td>$250.00</td>
                            <td class="text-center">
                                <span class="badge bg-info/20 text-info rounded-full hover:top-0">In Process</span>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
        <v-col>
            <v-dialog
                v-model="openDialog"
                transition="dialog-bottom-transition"
                width="35%"
            >
                <v-card>
                    <v-toolbar
                        color="primary"
                        class="elevation-0"
                        height="50px"
                    >
                        <div style="color:white; font-size:17px; font-weight:700;">Company 등록</div>
                        <v-spacer></v-spacer>
                        <v-icon
                            color="white"
                            small
                            @click="closeDialog()"
                        >mdi-close</v-icon>
                    </v-toolbar>
                    <v-card-text>
                        <Company :offline="offline"
                            :isNew="!itemToEdit"
                            :editMode="true"
                            v-model="value"
                            @add="append"
                            @edit="edit"
                        />
                    </v-card-text>
                </v-card>
            </v-dialog>
        </v-col>
        <v-col style="margin-bottom:40px;">
            <div class="text-center">
                <v-dialog
                    width="332.5"
                    fullscreen
                    hide-overlay
                    transition="dialog-bottom-transition"
                >
                    <v-btn
                        style="position:absolute; top:2%; right:2%"
                        @click="closeDialog()"
                        depressed
                        icon 
                        absolute
                    >
                        <v-icon>mdi-close</v-icon>
                    </v-btn>
                </v-dialog>
            </div>
        </v-col>
    </div>
</template>

<script>
import BaseEntity from './components/base-ui/BaseEntity.vue'

export default {
    name: 'companyGrid',
    mixins:[BaseEntity],
    components:{
    },
    data: () => ({
        path: 'companies',
    }),
    methods:{
        addNewRow(){
            this.openDialog = true;
        }
    }
}
</script>