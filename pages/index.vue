<template>
    <v-row justify="center" align="center">
    <v-col cols="12" sm="9" md="9"> 
        <v-card class="card">
            <v-form
            ref="form"
            v-model="form"
            @submit.prevent="onSubmit"
            >
            <div class="title">
                <v-list-item-title style="font-size: 24px;">{{ webinarName }}</v-list-item-title>
            <div style="display: flex;">
            <v-btn class="btnBack"
            color="error"
            @click="dialog = true">Назад</v-btn>
            <v-btn
            class="btnSafe"
            color="green"
            :disabled="!form"
            :loading="loading"
            >Сохранить</v-btn>
            </div>
            </div>
            <div class="nameWebinar">
                <v-text-field
                :rules="webinarNameRules"
                outlined
                label="Название вебинара"
                v-model="webinarName"
                ></v-text-field>
            </div>
            <div class="indexWebinar">
                <v-text-field
                v-model="webinarIndex"
                :rules="webinarIndexRules"
                outlined
                label="Идентификационный номер вебинара"
                ></v-text-field>
            </div>
        </v-form>
            <div class="gift">
                <h3>Подарки</h3>
                <v-btn
                color="primary"
                @click="addGift = true"
                >
                Добавить</v-btn>
            </div>

            <ul>
                <li style="margin-top: 20px; display: flex; justify-content: space-between;"  v-for="(gift, index) in gifts">
                    {{ gift }}
                    <v-btn color="error" @click="deleteGift = true">Удалить</v-btn>
                            <v-dialog 
                                v-model="deleteGift"
                                width="auto">
                                <v-card>
                                    <v-card-title>Подтверждение удаления</v-card-title>
                                    <v-card-text>Вы действительно хотите удалить данный подарок этот подарок?</v-card-text>
                                    <div style="display:flex; justify-content: flex-end;">
                                    <v-btn class="back" color="blue" @click="deleteGift = false">Назад</v-btn>
                                    <v-btn class="delete" color="error" @click="removeGift(index)">Удалить</v-btn>
                                </div>
                                </v-card>
                            </v-dialog>
                </li>
            </ul>

        </v-card>
        <v-dialog
    v-model="dialog"
    width="auto">
        <v-card width="400px">
            <v-card-title>Подтверждение ухода</v-card-title>
            <v-card-text>Вы действительно хотите вернуться к списку вебинаров? Внимание, все несохранённые изменения будут удалены.</v-card-text>
            <div class="flex">
            <v-btn color="green" text @click="dialog = false">Отмена</v-btn>
            <v-btn color="error" text @click="dialog = false">Назад</v-btn>
            </div>
        </v-card>
    </v-dialog>

    <v-dialog
    v-model="addGift"
    width="auto">
        <v-card class="addGift" width="800px">
            <v-card-title>{{ nameGift }}</v-card-title>
            <v-form
            ref="form"
            v-model="formAddGift"
            @submit.prevent="submitAddGift"
            >
            <v-text-field
            outlined
            label="Название подарка"
            v-model="nameGift"
            :rules="requered"></v-text-field>
            <div class="space">
            <v-text-field
            outlined
            label="Порядковый номер в очереди"
            v-model="numberGift"
            :rules="requered"></v-text-field>
            <v-text-field
            outlined
            label="Задержка в выдаче в секундах"
            v-model="delayGift"
            :rules="requered"></v-text-field>
            </div>
            <v-text-field
            outlined
            label="Ссылка на скачивание"
            v-model="linkGift"
            :rules="requered"></v-text-field>
            <v-btn 
            text
            color="error"
            @click="addGift = false">Назад</v-btn>
            <v-btn
            text
            color="green"
            @click="addNewGift"
            :disabled="!formAddGift"
            :loading="loading">Сохранить</v-btn>
        </v-form>
        </v-card>
    </v-dialog>

    </v-col>
    </v-row>
</template>

<script>
export default {
    data: () => ({
    deleteGift: false,
    formAddGift:false,
    nameGift:"",
    numberGift:"",
    delayGift:"",
    linkGift:"",
    requered:[(v) => !!v || "Обязательно к заполненнию"],
    addGift:false,
    dialog: false,
    webinarName: "",
    webinarNameRules: [(v) => !!v || "Обязательно к заполненнию"],
    webinarIndex: "",
    webinarIndexRules: [(v) => !!v || "Обязательно к заполненнию"],
    form: false,
    loading: false,
    gifts: []
    }),
    methods: {
        removeGift (index) {
            this.gifts.splice(index, 1)

            this.deleteGift = false
        },
        addNewGift () {
            this.gifts.push(this.nameGift)

            this.addGift = false

            this.nameGift = ''

            this.linkGift = ''

            this.numberGift = ''

            this.delayGift = ''
        },
        onSubmit () {
        if (!this.form) return

        this.loading = true

        setTimeout(() => (this.loading = false), 2000)
        },
        submitAddGift () {
            if (!this.formAddGift) return

            this.loading = true

            setTimeout(() => (this.loading = false), 2000)
        },
    },
}
</script>

<style>
    .delete, .back {
        margin: 20px;
    }
    .space {
        display: flex;
        justify-content: space-around;
    }
    .addGift {
        padding-top: 0;
        padding: 20px;
    }
    .flex {
        display: flex;
        justify-content: end;
    }
    .gift {
        margin-top: 40px;
        display: flex;
        justify-content: space-between;
    }
    .btnSafe {
        margin-left: 20px;
    }
    .title {
        display: flex;
        padding: 20px;
        justify-content: space-between;
    }
    .card {
        padding: 20px;
        padding-top: 0;
    }
</style>