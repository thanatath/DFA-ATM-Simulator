<template>
  <div id="navbar">
    <b-navbar toggleable="lg" type="dark" variant="dark" sticky>
        <b-navbar-toggle target="nav-collapse" ></b-navbar-toggle>
        
        <b-navbar-brand href="/" >
            <img src="../assets/icon.png" class="d-inline-block align-top ml-2" width="30rem" alt="logo">
            DFA-ATM
        </b-navbar-brand>

        <b-collapse id="nav-collapse" is-nav>
            <b-navbar-nav>
                <b-nav-item href="/" >หน้าแรก</b-nav-item>
                    
                    
                <b-nav-item v-b-modal.about>เกี่ยวกับเว็บไซต์</b-nav-item>
                    <b-modal id="about" centered title="เกี่ยวกับเว็บไซต์" style="font-family: 'Prompt', sans-serif;">
                        <ol>
                            <li></li>
                        </ol>
                    </b-modal>

                <b-nav-item v-b-modal.member >สมาชิก</b-nav-item>
                    <b-modal id="member" centered title="เกี่ยวกับเว็บไซต์" style="font-family: 'Prompt', sans-serif;">
                        <ol>
                            <li>นายสานตอก</li>
                            <li>นายยาม</li>
                            <li>นายน๊อต</li>
                            <li>นายโร</li>
                            <li>นายเสก</li>
                            <li>นายฟุก</li>
                        </ol>
                    </b-modal>
                
            </b-navbar-nav>
        </b-collapse>

        <b-navbar-nav class="ml-auto">
            <b-button variant="danger" size="sm" type="submit" v-on:click="reset">RESET</b-button>
        </b-navbar-nav>
    </b-navbar>
  </div>
</template>

<script>
export default {
    name:'Navbar',
    props: {
        reset: {
            type: Function
        }
    }
}
</script>


<style>

@import url('https://fonts.googleapis.com/css2?family=Prompt&display=swap');

#navbar {
    font-family: 'Prompt', sans-serif;
    width: 100%;
    position: fixed;
    z-index: 10;
}
</style>