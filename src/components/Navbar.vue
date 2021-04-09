<template>
  <div id="navbar">
    <b-navbar toggleable="lg" type="dark" variant="dark" sticky>
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-navbar-brand href="/">
        <img
          src="../assets/icon.png"
          class="d-inline-block align-top ml-2"
          width="30rem"
          alt="logo"
        />
        DFA-ATM
      </b-navbar-brand>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="/">หน้าแรก</b-nav-item>

          <b-nav-item v-b-modal.about>คำแนะนำการใช้งาน</b-nav-item>
          <b-modal
            id="about"
            centered
            title="เกี่ยวกับเว็บไซต์"
            style="font-family: 'Prompt', sans-serif;"
          >
            <ol>
              <li>เสียบบัตรATM</li>
              <li>กรอกรหัสผ่าน'123' จากนั้นกดตกลง</li>
              <li>กรอกจำนวนเงินที่ต้องการถอน จากนั้นกดตกลง</li>
              <li>รับเงิน</li>
            </ol>
          </b-modal>

          <b-nav-item v-b-modal.member>สมาชิก</b-nav-item>
          <b-modal
            id="member"
            centered
            title="สมาชิก"
            style="font-family: 'Prompt', sans-serif;"
          >
            <ol>
              <li>นายชญานิน บัวสละ รหัสนักศึกษา 62015021</li>
              <li>นายณัฐภูมิ ล้อมเขตร รหัสนักศึกษา 62015038</li>
              <li>นายทรงวุฒิ นักร้อง รหัสนักศึกษา 62015044</li>
              <li>นายธนธัช อัศวรัตนากร รหัสนักศึกษา 62015048</li>
              <li>นายเสกสรรค์ ทองอ่อน รหัสนักศึกษา 62015123</li>
              <li>นายอรรถพล ตันติวัฒนะผล รหัสนักศึกษา 62015131</li>
            </ol>
          </b-modal>
        </b-navbar-nav>
      </b-collapse>

      <b-navbar-nav class="ml-auto">
        <b-button variant="danger" size="sm" type="submit" v-on:click="reset"
          >RESET</b-button
        >
      </b-navbar-nav>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: 'Navbar',
  props: {
    reset: {
      type: Function,
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Prompt&display=swap');

#navbar {
  font-family: 'Prompt', sans-serif;
  width: 100%;
  position: fixed;
  z-index: 10;
}
ol{
  padding-left: 15px;
}
</style>
