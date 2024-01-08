<template>
  <div class="main">
    <div>
      <label class="label" for="fullname">Họ và tên:</label>
      <input class="input" v-model="fullname" id="fullname">
    </div>
    <div>
      <label class="label" for="role">Chức vụ:</label>
      <input class="input" v-model="role" id="role">
    </div>
    <div>
      <label class="label" for="phone_number">Số điện thoại:</label>
      <input class="input" v-model="phone_number" id="phone_number">
    </div>
    <div>
      <label class="label" for="email">Email:</label>
      <input class="input" v-model="email" id="email">
    </div>
  </div>
  <div class="center">
    <button class="label" @click="copySignature">Sao chép Chữ ký</button>
  </div>
  <table class="signature-section" id="signature-section">
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
                      <img src="https://i.imgur.com/pN5ZdYD.png" alt="facebook" class="sub-logo-img">
                    </a>
                    <a v-if="companyInfo.linkedin" :href="companyInfo.fanpage" class="sub-logo ml-5" target="_blank" :data-saferedirecturl="companyInfo.linkedin">
                      <img src="https://i.imgur.com/2xOKI0F.png" alt="linkedin" class="sub-logo-img">
                    </a>
                    <a v-if="companyInfo.twitter" :href="companyInfo.fanpage" class="sub-logo ml-5" target="_blank" :data-saferedirecturl="companyInfo.twitter">
                      <img src="https://i.imgur.com/uRHrvU4.png" alt="twitter" class="sub-logo-img">
                    </a>
                    <a v-if="companyInfo.instagram" :href="companyInfo.fanpage" class="sub-logo ml-5" target="_blank" :data-saferedirecturl="companyInfo.instagram">
                      <img src="https://i.imgur.com/3tgNopu.png" alt="instagram" class="sub-logo-img">
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
                          <span width="11">
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
  <div style="text-align: center">
    <span class="text-center">Hướng dẫn cách thêm chữ ký vào mail 
    <a style="font-weight: bold" href="https://support.google.com/mail/answer/8395?hl=vi&co=GENIE.Platform%3DDesktop&oco=0" target="blank"> tại đây </a>
    </span>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

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
  logo: 'https://i.imgur.com/DUimh2m.png'
};

var contactInfo = [
  { label: 'Phone', value: phone_number.value, type: 'tel', icon: 'https://i.imgur.com/5SZWbkX.png' },
  { label: 'Email', value: email.value, type: 'email', icon: 'https://i.imgur.com/AMP3sZX.png' },
  { label: 'Website', value: companyInfo.website, type: 'link', icon: 'https://i.imgur.com/qX4L3XC.png' },
  { label: 'Address', value: companyInfo.address, type: 'address', icon: 'https://i.imgur.com/KxTc7E7.png' },
];

watch(phone_number, (newVal) => {
  contactInfo.find(item => item.label === 'Phone').value = newVal;
});

watch(email, (newVal) => {
  contactInfo.find(item => item.label === 'Email').value = newVal;
});

const copySignature = () => {
  const signatureOutput = document.getElementById('signature-section');
  const range = document.createRange();
  range.selectNode(signatureOutput);
  window.getSelection().removeAllRanges();
  window.getSelection().addRange(range);
  document.execCommand('copy');
  window.getSelection().removeRange(range);
  alert('Chữ ký đã được sao chép!');
}
</script>

<style>
  html, p, a, span, h3 {
    font-family: 'Times New Roman', Times, serif;
    font-size: 12px;
    color: black;
  }

  .label {
    font-size: 15px;
    font-weight: 700;
  }

  .input {
    width: 100%;
    margin: 5px 0 10px;
  }

  .main {
    border-bottom:1px solid rgb(20,59,115);
    margin: 0 auto;
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

  .center {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 50px;
  }
</style>
