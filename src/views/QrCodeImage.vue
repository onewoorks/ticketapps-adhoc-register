<template>
    <v-container >
        <v-card v-for="(ticket, index) in tickets" :key="index" 
            class='text-center qrcode_card' >
            <center>
        <v-img src='/images/events/4/teraju-logo.jpg' alt="" width="300px"/>
        <div style="font-weight:bold; font-size: 1.3em">{{ event_detail.event_info.event_name.toUpperCase() }}</div>
        
        <v-img src='/images/events/4/logo-jana.png' alt="" width="130px" />
      </center>
            <qrcode 
                :value="ticket.event_code+'-'+ticket.id+'-'+ticket.register_code" 
                :options="{ width: 200 }" style="z-index:1; position:relative"></qrcode> 
            <v-card-text style="position:relative; color:#000000; z-index:1">
                <div class='qrcode_code'>{{ ticket.qr_code.toUpperCase() }}</div>
                <div class='qrcode_name'>{{ ticket.fullname.toUpperCase() }}</div>  
            <div>{{ ticket.email }}</div>
            <div>{{ ticket.phone_no}}</div>
            <div>{{ ticket.identification_no}}</div>    
            </v-card-text>

             <v-img src='/images/events/4/janadoc.jpg' style="opacity:0.5; margin-top:-100px" />
          <v-img src='/images/events/4/ticket-apps.jpg' width="100px" style="position:absolute; bottom:10px; right:10px"/>
        </v-card>
        
    </v-container>
</template>

<script>
    import VueQrcode from '@chenfengyuan/vue-qrcode';
    export default {
        data: function(){
            return { 
                tickets : [],
                event_detail : null
            }
        },
        components: {
            "qrcode": VueQrcode
        },
        methods: {
            add_to_local_storage: function(tickets, events){
                let qrcode_info = {
                    events: events,
                    tickets: tickets
                }
                localStorage.setItem('confirmed_qrcode', JSON.stringify(qrcode_info));
            }
        },
        mounted: function(){
            this.tickets = this.$route.params.persons.data
            this.event_detail = this.$route.params.events
            this.add_to_local_storage(this.tickets, this.event_detail)
        }
    }
</script>

<style lang="scss" scoped>
    .qrcode_code {
        font-weight : bold;
        font-size   : 1.5em
    }
    .qrcode_name {
        font-size: 1.3em;
        padding-top:10px;
    }

    .qrcode_card {
        margin-bottom: 20px;
    }

</style>