<template>
  <div id="app">
    
    <Navbar :reset="this.reset" />
    <v-parallax height="2000" src="https://firebasestorage.googleapis.com/v0/b/imgatm.appspot.com/o/BG.png?alt=media&token=6e884c2f-0c2f-49b3-bad6-5707db51dbe5">
    <b-container fluid>
      <b-row class="text-center pt-5">

        <b-col sm="6" class="atm p-4">
          <h1 style="color:white;">ATM : Automatic Teller Machine</h1>
          <b-row class="justify-content-md-center">
            <b-col cols="11" class="bodyATM">
              <!--1st-->
              <b-row class="first p-3 justify-content-between">
                <b-col cols="2" align="center" align-self="center">
                   
                  <vue-web-cam
                    ref="webcam"
                    class="mirror"
                    v-b-tooltip.hover title="กระจกระวังหลัง" 
                    :device-id="deviceId"
                    width="100%"
                    @started="onStarted"
                    @stopped="onStopped"
                    @error="onError"
                    @cameras="onCameras"
                    @camera-change="onCameraChange"
                  />
                  <!-- <div class="mirror" id="mirrorLeft"> </div> //add comment old mirror for use webcam --> 
                </b-col>

                <!-- <b-col cols="1" align="center" align-self="center">
                  <div class="camera" id="camera"></div>
                  <b-tooltip target="camera" triggers="hover" variant="primary"
                    >กล้องวงจรปิด</b-tooltip
                  >
                </b-col> -->
                 

                <!-- <select v-model="camera"> //Section for option to select Camera device
                  <option>-- Select Device --</option>
                  <option
                    v-for="device in devices"
                    :key="device.deviceId"
                    :value="device.deviceId"
                    >{{ device.label }}</option
                  >
                </select> -->
                
                <b-col cols="2" align="center" align-self="center">
                  <!-- <div class="mirror" id="mirrorRight"></div>  //add comment old mirror for use webcam -->
                                    <vue-web-cam
                    ref="webcam"
                    class="mirror"
                    v-b-tooltip.hover title="กระจกระวังหลัง" 
                    :device-id="deviceId"
                    width="100%"
                    @started="onStarted"
                    @stopped="onStopped"
                    @error="onError"
                    @cameras="onCameras"
                    @camera-change="onCameraChange"
                  />
                  <!-- <b-tooltip
                    target="mirrorRight"
                    triggers="hover"
                    variant="primary"
                    >กระจกระวังหลัง</b-tooltip
                  > -->
                </b-col>
              </b-row>

              <!--2nd-->
              <b-row class="second py-4">
                <b-col cols="2"></b-col>

                <!--Monitor-->
                <b-col cols="8" class="monitor text-left">
                  <p class="p-1">ธนาคารทรงวุฒิไทย</p>
                  <h2 class="text-center pt-5">{{ title }}</h2>
                  <h5 class="text-center pb-3">{{ subTitle }}</h5>

                  <b-row align-h="center">
                    <b-col cols="7">
                      <b-form-input
                        disabled
                        v-model="input"
                        v-if="showInput"
                        id="input"
                        class="text-center"
                        size="lg"
                      >
                      </b-form-input>
                    </b-col>
                  </b-row>
                </b-col>

                <b-col cols="2" class="rightButton" align-self="end">
                  <b-button v-on:click="edit" size="lg" variant="warning" block
                    >แก้ไข</b-button
                  >
                  <b-button
                    v-on:click="accept"
                    size="lg"
                    variant="success"
                    block
                    class="my-4"
                    >ตกลง</b-button
                  >
                  <b-button v-on:click="reset" size="lg" variant="danger" block
                    >ยกเลิก</b-button
                  >
                </b-col>
              </b-row>

              <!--3rd-->
              <b-row class="third py-4">
                <b-col cols="3"></b-col>

                <!--Numpad-->
                <b-col cols="6" class="px-3">
                  <b-row align-h="center" class="p-2 pt-4 numpad">
                    <b-col v-on:click="num1" cols="4" class="pb-4"
                      ><b-button block size="lg">1</b-button></b-col
                    >
                    <b-col v-on:click="num2" cols="4"
                      ><b-button block size="lg">2</b-button></b-col
                    >
                    <b-col v-on:click="num3" cols="4"
                      ><b-button block size="lg">3</b-button></b-col
                    >

                    <b-col v-on:click="num4" cols="4" class="pb-4"
                      ><b-button block size="lg">4</b-button></b-col
                    >
                    <b-col v-on:click="num5" cols="4"
                      ><b-button block size="lg">5</b-button></b-col
                    >
                    <b-col v-on:click="num6" cols="4"
                      ><b-button block size="lg">6</b-button></b-col
                    >

                    <b-col v-on:click="num7" cols="4" class="pb-4"
                      ><b-button block size="lg">7</b-button></b-col
                    >
                    <b-col v-on:click="num8" cols="4"
                      ><b-button block size="lg">8</b-button></b-col
                    >
                    <b-col v-on:click="num9" cols="4"
                      ><b-button block size="lg">9</b-button></b-col
                    >

                    <b-col v-on:click="num0" cols="4" class="pb-3"
                      ><b-button block size="lg">0</b-button></b-col
                    >
                  </b-row>
                </b-col>

                <!--Card-->
                <b-col cols="3" align="center">
                  <div class="cardSlot" id="cardSlot"></div>
                  <div
                    class="atmCard pt-5 shadow-sm"
                    id="card"
                    v-if="showCard"
                    v-on:click="card"
                  >
                    <p>ธนาคารทรงวุฒิไทย</p>
                    <p><small>5587 2221 8877 6685</small></p>
                    <p>VISA</p>
                  </div>
                  <b-tooltip target="card" triggers="hover" variant="primary"
                    >บัตร ATM</b-tooltip
                  >
                  <b-tooltip
                    target="cardSlot"
                    triggers="hover"
                    variant="primary"
                    >ช่องใส่บัตร ATM</b-tooltip
                  >
                </b-col>
              </b-row>

              <!--4th-->
              <b-row class="fourth p-5" align-h="center">
                <div class="moneySlot" id="moneySlot"></div>
                <b-tooltip target="moneySlot" triggers="hover" variant="primary">ช่องเงินออก</b-tooltip>

                <div v-on:click="money" class="money pt-5" id="money" v-if="showMoney">
                  <h1>{{withdrawn}} บาท</h1>
                  <b-tooltip target="money" triggers="hover" variant="primary">คลิกเพื่อรับเงิน</b-tooltip>
                </div>
                

              </b-row>

              <!--5th-->
              <b-row class="fifth pr-3" align-v="end" align-h="end">
                <h1>ธนาคารทรงวุฒิไทย</h1>
              </b-row>
            </b-col>
          </b-row>
        </b-col>

        <b-col sm="6" class="dfa p-4">
          <h1>DFA : Deterministic Finite Automata</h1>
          <p>currentState = {{this.state}}</p>
          <img src="./assets/noState.svg" alt="dfa" />
        </b-col>
        
      </b-row>
    </b-container>
</v-parallax>
    <Footer />
    
  </div>
</template>

<script>
import Navbar from './components/Navbar';
import Footer from './components/Footer';
import { WebCam } from 'vue-web-cam';

export default {
  name: 'Home',
  components: {
    Navbar,
    Footer,
    'vue-web-cam': WebCam,
  },
  data() {
    return {
      title: 'ยินดีต้อนรับ',
      subTitle: 'กรุณาใส่บัตรเพื่อเริ่มทำรายการ',
      input: '',
      state: 0,
      img: null,
      camera: null,
      deviceId: null,
      devices: [],
      withdrawn: 0,
      showInput: false,
      showMoney: false,
      showCard: true,

      currentState: '',
    };
  },
  methods: {
    //Reset
    reset: function() {
      this.title = 'ยินดีต้อนรับ';
      this.subTitle = 'กรุณาใส่บัตรเพื่อเริ่มทำรายการ';
      this.input = '';
      this.state = 0;

      this.withdrawn = 0;
      this.showInput = false;
      this.showMoney = false;
      this.showCard = true;

      this.currentState = '';
    },

    //Menu
    edit: function() {
      //แก้ไขรหัสผ่าน
      if(this.state >= 1 && this.state <= 4 || this.state === 13) {
        this.state = 1;
        this.title = 'กรุณาป้อนรหัสผ่าน';
        this.subTitle = '';
        this.showInput = true;
        this.showCard = false;
        this.input = ''
      }

      //แก้ไขจำนวนเงิน
      else if(this.state >= 5 && this.state <= 9 || this.state >= 16 && this.state <= 18) {
        this.state = 5
        this.input = ''
        this.title = 'กรุณาป้อนจำนวนเงินที่ต้องการถอน'
      }
    },
    accept: function() {
      //ใส่รหัส 123 ถูกต้อง
      if(this.state === 4 && this.input === '123') {
        this.state = 5
        this.input = ''
        this.title = 'กรุณาป้อนจำนวนเงินที่ต้องการถอน'
      }

      //ใส่รหัสไม่ถูกต้อง
      else if (this.state === 2 || this.state === 3 || this.state === 13) {
        this.state = 15
        this.input = ''
        this.showInput = false
        this.title = 'รหัสผ่านไม่ถูกต้อง'
        this.subTitle = 'กดยืนยันเพื่อป้อนรหัสใหม่'
      }

      //รหัสผ่านไม่ถูกต้อง ป้อนรหัสผ่านใหม่
      else if (this.state === 15 ) {
        this.state = 1
        this.title = 'กรุณาป้อนรหัสผ่าน'
        this.subTitle = ''
        this.showInput = true
        this.showCard = false
      }


      //ถอนเงินสำเร็จ
      else if(this.state === 8 || this.state === 9) {
        this.state = 10
        this.title = 'ถอนเงินสำเร็จกรุณารับบัตรคืน'
        this.subTitle = 'ขอบคุณที่ใช้บริการ'
        this.withdrawn = this.input
        this.showInput = false
        this.showCard = true
        this.showMoney = true
      }

      //ใส่จำนวนเงินไม่ถูกต้อง
      else if(this.state === 6 || this.state === 7 || this.state === 16 || this.state === 17 || this.state === 18 ) {
        this.state = 19
        this.title = 'จำนวนเงินไม่ถูกต้อง'
        this.subTitle = 'กดยืนยันเพื่อป้อนจำนวนเงินใหม่'
        this.showInput = false
        this.input = ''
      }

      //จำนวนเงินไม่ถูกต้อง ป้อนจำนวนเงินใหม่
      else if(this.state === 19) {
        this.state = 5
        this.input = ''
        this.title = 'กรุณาป้อนจำนวนเงินที่ต้องการถอน'
        this.subTitle = ''
        this.showInput = true
      }
    },
    cancel: function() {},

    //Card & Money
    card: function() {
      if (this.state === 0) {
        this.state = 1;
        this.title = 'กรุณาป้อนรหัสผ่าน';
        this.subTitle = '';
        this.showInput = true;
        this.showCard = false;
      }

      else if (this.state === 10) {
        this.reset();
      }
    },
    money: function() {
      if (this.state === 10) {
        this.showMoney = false;
      }
    },

    //Numpad
    num1: function() {
      //รหัสผ่านถูก (ตัวที่ 1)
      if(this.state === 1) {
        this.state = 2
        this.input = this.input.concat('1')
      }

      //รหัสผ่านผิด
      else if(this.state === 13 || this.state === 2 || this.state === 3 ||  this.state === 4) {
        this.state = 13
        this.input = this.input.concat('1')
      }

      //ถอนเงิน
      else if(this.state === 5) {
        this.state = 6
        this.input = this.input.concat('1')
      }

      //จำนวนเงินไม่ถูกต้อง
      else if(this.state === 6 || this.state === 7 || this.state === 8) {
        this.state = 16
        this.input = this.input.concat('1')
      }
      
      //จำนวนเงินไม่ถูกต้อง (หลักที่3)
      else if(this.state === 16) {
        this.state = 17
        this.input = this.input.concat('1')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักสุดท้าย)
      else if(this.state === 17) {
        this.state = 18
        this.input = this.input.concat('1')
      }
    },
    num2: function() {
      //รหัสผ่านผิด
      if(this.state === 13 || this.state === 1 || this.state === 3 || this.state === 4) {
        this.state = 13
        this.input = this.input.concat('2')
      }

      //รหัสผ่านถูก (ตัวที่ 2)
      else if(this.state === 2) {
        this.state = 3
        this.input = this.input.concat('2')
      }

      //ถอนเงิน
      else if(this.state === 5) {
        this.state = 6
        this.input = this.input.concat('2')
      }

      //จำนวนเงินไม่ถูกต้อง
      else if(this.state === 6 || this.state === 7 || this.state === 8) {
        this.state = 16
        this.input = this.input.concat('2')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักที่3)
      else if(this.state === 16) {
        this.state = 17
        this.input = this.input.concat('2')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักสุดท้าย)
      else if(this.state === 17) {
        this.state = 18
        this.input = this.input.concat('2')
      }
    },
    num3: function() {
      //รหัสผ่านผิด
      if(this.state === 13 || this.state === 1 || this.state === 2 || this.state === 4) {
        this.state = 13
        this.input = this.input.concat('3')
      }

      //รหัสผ่านถูก (ตัวที่ 3)
      else if(this.state === 3) {
        this.state = 4
        this.input = this.input.concat('3')
      }

      //ถอนเงิน
      else if(this.state === 5) {
        this.state = 6
        this.input = this.input.concat('3')
      }

      //จำนวนเงินไม่ถูกต้อง
      else if(this.state === 6 || this.state === 7 || this.state === 8) {
        this.state = 16
        this.input = this.input.concat('3')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักที่3)
      else if(this.state === 16) {
        this.state = 17
        this.input = this.input.concat('3')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักสุดท้าย)
      else if(this.state === 17) {
        this.state = 18
        this.input = this.input.concat('3')
      }
    },
    num4: function() {
      //รหัสผ่านผิด
      if(this.state === 13 || this.state >= 1 && this.state <= 4) {
        this.state = 13
        this.input = this.input.concat('4')
      }

      //ถอนเงิน
      else if(this.state === 5) {
        this.state = 6
        this.input = this.input.concat('4')
      }

      //จำนวนเงินไม่ถูกต้อง
      else if(this.state === 6 || this.state === 7 || this.state === 8) {
        this.state = 16
        this.input = this.input.concat('4')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักที่3)
      else if(this.state === 16) {
        this.state = 17
        this.input = this.input.concat('4')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักสุดท้าย)
      else if(this.state === 17) {
        this.state = 18
        this.input = this.input.concat('4')
      }
    },
    num5: function() {
      //รหัสผ่านผิด
      if(this.state === 13 || this.state >= 1 && this.state <= 4) {
        this.state = 13
        this.input = this.input.concat('5')
      }

      //ถอนเงิน
      else if(this.state === 5) {
        this.state = 6
        this.input = this.input.concat('5')
      }

      //จำนวนเงินไม่ถูกต้อง
      else if(this.state === 6 || this.state === 7 || this.state === 8) {
        this.state = 16
        this.input = this.input.concat('5')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักที่3)
      else if(this.state === 16) {
        this.state = 17
        this.input = this.input.concat('5')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักสุดท้าย)
      else if(this.state === 17) {
        this.state = 18
        this.input = this.input.concat('5')
      }
    },
    num6: function() {
      //รหัสผ่านผิด
      if(this.state === 13 || this.state >= 1 && this.state <= 4) {
        this.state = 13
        this.input = this.input.concat('6')
      }

      //ถอนเงิน
      else if(this.state === 5) {
        this.state = 6
        this.input = this.input.concat('6')
      }

      //จำนวนเงินไม่ถูกต้อง
      else if(this.state === 6 || this.state === 7 || this.state === 8) {
        this.state = 16
        this.input = this.input.concat('6')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักที่3)
      else if(this.state === 16) {
        this.state = 17
        this.input = this.input.concat('6')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักสุดท้าย)
      else if(this.state === 17) {
        this.state = 18
        this.input = this.input.concat('7')
      }
    },
    num7: function() {
      //รหัสผ่านผิด
      if(this.state === 13 || this.state >= 1 && this.state <= 4) {
        this.state = 13
        this.input = this.input.concat('7')
      }
      
      //ถอนเงิน
      else if (this.state === 5) {
        this.state = 6;
        this.input = this.input.concat('7');
      }

      //จำนวนเงินไม่ถูกต้อง
      else if(this.state === 6 || this.state === 7 || this.state === 8) {
        this.state = 16
        this.input = this.input.concat('7')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักที่3)
      else if(this.state === 16) {
        this.state = 17
        this.input = this.input.concat('7')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักสุดท้าย)
      else if(this.state === 17) {
        this.state = 18
        this.input = this.input.concat('7')
      }
    },
    num8: function() {
      //รหัสผ่านผิด
      if(this.state === 13 || this.state >= 1 && this.state <= 4) {
        this.state = 13
        this.input = this.input.concat('8')
      }

      //ถอนเงิน
      else if (this.state === 5) {
        this.state = 6;
        this.input = this.input.concat('8');
      }

      //จำนวนเงินไม่ถูกต้อง
      else if(this.state === 6 || this.state === 7 || this.state === 8) {
        this.state = 16
        this.input = this.input.concat('8')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักที่3)
      else if(this.state === 16) {
        this.state = 17
        this.input = this.input.concat('8')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักสุดท้าย)
      else if(this.state === 17) {
        this.state = 18
        this.input = this.input.concat('8')
      }
    },
    num9: function() {
      //รหัสผ่านผิด
      if(this.state === 13 || this.state >= 1 && this.state <= 4) {
        this.state = 13
        this.input = this.input.concat('9')
      }

      //ถอนเงิน
      else if (this.state === 5) {
        this.state = 6;
        this.input = this.input.concat('9');
      }

      //จำนวนเงินไม่ถูกต้อง
      else if(this.state === 6 || this.state === 7 || this.state === 8) {
        this.state = 16
        this.input = this.input.concat('9')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักที่3)
      else if(this.state === 16) {
        this.state = 17
        this.input = this.input.concat('9')
      }

      //จำนวนเงินไม่ถูกต้อง (หลักสุดท้าย)
      else if(this.state === 17) {
        this.state = 18
        this.input = this.input.concat('9')
      }
    },
    num0: function() {
      //รหัสผ่านผิด
      if(this.state === 13 || this.state >= 1 && this.state <= 4) {
        this.state = 13
        this.input = this.input.concat('0')
      }

      //ถอนเงิน
      else if(this.state >= 6 && this.state < 9) {
        this.state += 1
        this.input = this.input.concat('0')
      }

      //จำนวนเงินเกิน 3 หลัก

      //จำนวนเงินไม่ถูกต้อง (0 หลักที่ 3 // หลังเลข 1-9 เช่น 220)
      else if(this.state === 16) {
        this.state = 17
        this.input = this.input.concat('0')
      }
      
      //จำนวนเงินถูกต้อง (0 หลักที่ 4 // หลังเลข 1-9 เช่น 2200)
      else if(this.state === 17) {
        this.state = 9
        this.input = this.input.concat('0')
      }
    },

    // start webcam method path
    onCapture() {
      this.img = this.$refs.webcam.capture();
    },
    onStarted(stream) {
      console.log('On Started Event', stream);
    },
    onStopped(stream) {
      console.log('On Stopped Event', stream);
    },
    onStop() {
      this.$refs.webcam.stop();
    },
    onStart() {
      this.$refs.webcam.start();
    },
    onError(error) {
      console.log('On Error Event', error);
    },
    onCameras(cameras) {
      this.devices = cameras;
      console.log('On Cameras Event', cameras);
    },
    onCameraChange(deviceId) {
      this.deviceId = deviceId;
      this.camera = deviceId;
      console.log('On Camera Change Event', deviceId);
    },
    // end webcam method path
  },
  //computed & watch added for camera work
  computed: {
    device: function() {
      return this.devices.find((n) => n.deviceId === this.deviceId);
    },
  },
  //computed & watch added for camera work
  watch: {
    camera: function(id) {
      this.deviceId = id;
    },
    devices: function() {
      // Once camera we have a list select the first one
      const [first, ...tail] = this.devices;
      if (first) {
        this.camera = first.deviceId;
        this.deviceId = first.deviceId;
      }
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Prompt&display=swap');

#app {
  font-family: 'Prompt', sans-serif;
  /* background-color: aquamarine; */
  background: url('./assets/bg.png');
  background-size: contain;
  background-attachment: fixed;
  width: 1920px;
}

.atm {
  color: #212121;
}

.bodyATM {
  border: 15px solid #333;
  border-radius: 10px;
  width: 100%;
}

.first {
  background-color: black;
}

.mirror {
  border-radius: 10px;
  background: rgb(255, 255, 255);
  background: linear-gradient(
    135deg,
    rgba(255, 255, 255, 1) 0%,
    rgba(167, 167, 167, 1) 100%
  );
  width: 5vw;
  height: 10vh;
}

.camera {
  border: 3px solid rgb(66, 66, 66);
  border-radius: 20px;
  background-color: grey;
  width: 1vw;
  height: 2vh;
}

.second {
  background-color: grey;
}

.monitor {
  border: 10px solid #333;
  border-radius: 10px;
  background-color: royalblue;
  width: 100vh;
  height: 50vh;
}

.monitor h2,
.monitor h5 {
  color: white;
}

.menu {
  height: 22vh;
}

.third {
  border-top: 1px solid black;
  border-bottom: 1px solid black;
  background-color: grey;
}

.numpad {
  background-color: #333;
  border-radius: 8px;
}

.cardSlot {
  background-color: black;
  border: 10px solid #333;
  width: 100%;
  height: 4vh;
}

.atmCard {
  background-color: white;
  border: 5px solid rgb(245, 245, 245);
  border-radius: 10px;
  width: 80%;
  height: 22vh;
  top: -20px;
  position: relative;
}

.atmCard:hover {
  border: 5px solid red;
  cursor: pointer;
}

.fourth {
  background-color: grey;
  border-bottom: 1px solid black;
  height: 28vh;
}

.moneySlot {
  border: 10px solid #333;
  background-color: black;
  width: 70%;
  height: 4vh;
}

.money {
  background-color: white;
  border: 5px solid rgb(254, 254, 254);
  width: 60%;
  height: 18vh;
  top: -20px;
  position: relative;
}

.money:hover {
  border: 5px solid red;
  cursor: pointer;
}

.fifth {
  height: 60vh;
  background-color: royalblue;
}

.dfa {
  background-color: rgba(0, 0, 0, 0.9);
  color: white;
}
</style>
