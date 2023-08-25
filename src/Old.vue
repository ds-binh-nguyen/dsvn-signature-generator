<template>

    <div class="unselectable main">
      <div>
        <label for="fullname">Họ và tên:</label>
        <input class="input" v-model="fullname" id="fullname">
      </div>
      <div>
        <label for="role">Chức vụ:</label>
        <input class="input" v-model="role" id="role">
      </div>
      <div>
        <label for="phone_number">Số điện thoại:</label>
        <input class="input" v-model="phone_number" id="phone_number">
      </div>
      <div>
        <label for="email">Email:</label>
        <input class="input" v-model="email" id="email">
      </div>
    </div>
  
    <table class="signature-section">
      <tbody>
        <tr>
          <td>
            <td style="vertical-align:top">
              <table style="margin-top: 10px;">
                <tbody>
                  <tr>
                    <td style="text-align:center">
                      <img :src="companyInfo.logo" alt="diamge-share-logo" width="100" class="main-logo">
                      <a v-if="companyInfo.fanpage" :href="companyInfo.fanpage" class="sub-logo" target="_blank" :data-saferedirecturl="companyInfo.fanpage">
                        <img src="/img/facebook-icon-2x.webp" alt="facebook" class="sub-logo-img">
                      </a>
                      <a v-if="companyInfo.linkedin" :href="companyInfo.fanpage" class="sub-logo ml-5" target="_blank" :data-saferedirecturl="companyInfo.linkedin">
                        <img src="/img/linkedin-icon-2x.webp" alt="linkedin" class="sub-logo-img">
                      </a>
                      <a v-if="companyInfo.twitter" :href="companyInfo.fanpage" class="sub-logo ml-5" target="_blank" :data-saferedirecturl="companyInfo.twitter">
                        <img src="/img/twitter-icon-2x.webp" alt="twitter" class="sub-logo-img">
                      </a>
                      <a v-if="companyInfo.instagram" :href="companyInfo.fanpage" class="sub-logo ml-5" target="_blank" :data-saferedirecturl="companyInfo.instagram">
                        <img src="/img/instagram-icon-2x.webp" alt="instagram" class="sub-logo-img">
                      </a>
                    </td>
                  </tr>
                </tbody>
              </table>
            </td>
            <td>
              <h3 class="name title">{{ fullname }}</h3>
              <p class="title">{{ role }}</p>
              <p class="title">{{ companyInfo.name }}</p>
              <table>
                <tbody>
                  <tr>
                    <td class="break-line"></td>
                  </tr>
                </tbody>
              </table>
              <table>
                <tbody>
                  <tr v-for="item in contactInfo" :key="item.label" height="25" style="vertical-align:middle">
                    <td width="30" style="vertical-align:middle">
                      <table>
                        <tbody>
                          <tr>
                            <span width="11" class="icon-info">
                              <img :src="item.icon" :alt="item.label" width="13" class="icon-info">
                            </span>
                          </tr>
                        </tbody>
                      </table>
                    </td>
                    <td>
                      <template v-if="item.type === 'tel'">
                        <a :href="'tel:' + formattedPhone(companyInfo.phone).tel" target="_blank">{{ formattedPhone(companyInfo.phone).label }}</a>
                        &nbsp;|&nbsp;
                        <a :href="'tel:' + formattedPhone(item.value).tel" target="_blank">{{ formattedPhone(item.value).label }}</a>
                      </template>
                      <a v-else-if="item.type === 'email'" :href="'mailto:' + item.value" target="_blank">{{ item.value }}</a>
                      <a v-else-if="item.type === 'link'" :href="item.value" target="_blank">{{ item.value }}</a>
                      <span v-else>{{ item.value }}</span>
                    </td>
                  </tr>
                </tbody>
              </table>
              <br>
            </td>
          </td>
        </tr>
      </tbody>
    </table>
  </template>
  
  <script setup>
  import { ref, watch, onMounted, onBeforeUnmount } from 'vue'
  
  const fullname = ref('Nguyen Truong Binh');
  const role = ref('Developer');
  const phone_number = ref('0333160028');
  const email = ref('binh-nguyen@dimage.co.jp');
  
  const formattedPhone = (phone) => {
    const tel = `+84${phone.slice(1)}`;
    const label = `(+84) ${phone.slice(1, 4)}-${phone.slice(4, 7)}-${phone.slice(7)}`;
    return { tel, label };
  };
  
  const companyInfo = {
    name: 'DIMAGE SHARE VIETNAM CO., LTD',
    address: '11F, Lilama Building 10, 56 To Huu, Trung Van, Nam Tu Liem, Hanoi, Vietnam',
    phone: '02432005576',
    fanpage: 'https://www.facebook.com/DimageShareVietnam/',
    linked: '',
    instagram: '',
    twitter: '',
    website: 'https://dimage.vn/',
    logo: '/img/dsvn-logo.png'
  };
  
  var contactInfo = [
    { label: 'Phone', value: phone_number.value, type: 'tel', icon: '/img/phone-icon-2x.webp' },
    { label: 'Email', value: email.value, type: 'email', icon: '/img/email-icon-2x.webp' },
    { label: 'Website', value: companyInfo.website, type: 'link', icon: '/img/link-icon-2x.webp' },
    { label: 'Address', value: companyInfo.address, type: 'address', icon: '/img/address-icon-2x.webp' },
  ];
  
  watch(phone_number, (newVal) => {
    contactInfo.find(item => item.label === 'Phone').value = newVal;
  });
  
  watch(email, (newVal) => {
    contactInfo.find(item => item.label === 'Email').value = newVal;
  });
  
  const onKeyDown = (event) => {
    if (event.ctrlKey && event.key === 'a') {
      toggleInputVisibility();
    }
  };
  
  const toggleInputVisibility = () => {
    const inputElements = document.getElementsByTagName('input');
    for (let i = 0; i < inputElements.length; i++) {
      inputElements[i].style.display = inputElements[i].style.display === 'none' ? 'block' : 'none';
    }
  };
  
  onMounted(() => {
    document.addEventListener('keydown', onKeyDown);
  });
  
  onBeforeUnmount(() => {
    document.removeEventListener('keydown', onKeyDown);
  });
  </script>
  
  <style>
  html, p, a, span, h3 {
    font-family: 'Times New Roman', Times, serif;
    font-size: 12px;
    color: black;
  }
  
  .input {
    width: 100%;
    margin-bottom: 10px;
  }
  
  .unselectable {
    -webkit-user-select: none;
    -webkit-touch-callout: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }
  
  .main {
    border-bottom:1px solid rgb(20,59,115);
    margin-bottom: 100px;
    width: 50%;
  }
  
  .main-logo {
    max-width:100px;
    display:block
  }
  
  .sub-logo {
    color: #6A78D1;
    display:inline-block;
    padding:0px;
    background-color:#6A78D1
  }
  
  .ml-5 {
    margin-left: 5px;
  }
  
  .signature-section {
    color: #fff;
    vertical-align:-webkit-baseline-middle;
  }
  
  .sub-logo-img {
    color:#6A78D1;
    height:24px;
    max-width:135px;
    display:block;
  }
  
  .title {
    margin: 0px;
  }
  
  .mb-2 {
    margin-bottom: 2px;
  }
  
  .name {
    font-size: 16px;
  }
  
  .title {
    margin: 0 0 5px 0;
  }
  
  .break-line {
    width:459px;
    border-bottom:1px solid rgb(20,59,115);
    border-left:none;
    display:block;
  }
  
  .icon-info {
    display:block;
    background-color:rgb(20,59,115);
  }
  </style>
  