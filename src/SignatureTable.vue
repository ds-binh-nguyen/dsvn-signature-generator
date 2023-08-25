<template>
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
  import { defineProps } from 'vue';
  
  const { companyInfo, contactInfo } = defineProps(['companyInfo', 'contactInfo']);
  
  const formattedPhone = (phone) => {
    const tel = `+84${phone.slice(1)}`;
    const label = `(+84) ${phone.slice(1, 4)}-${phone.slice(4, 7)}-${phone.slice(7)}`;
    return { tel, label };
  };
  </script>
  
  <style>
  /* CSS cho component SignatureTable */
  .main-logo {
    max-width: 100px;
    display: block;
  }
  
  .sub-logo {
    color: #6A78D1;
    display: inline-block;
    padding: 0;
    background-color: #6A78D1;
  }
  
  .ml-5 {
    margin-left: 5px;
  }
  
  .signature-section {
    color: #fff;
    vertical-align: -webkit-baseline-middle;
  }
  
  .sub-logo-img {
    color: #6A78D1;
    height: 24px;
    max-width: 135px;
    display: block;
  }
  
  .title {
    margin: 0;
  }
  
  .break-line {
    width: 459px;
    border-bottom: 1px solid rgb(20, 59, 115);
    border-left: none;
    display: block;
  }
  
  .icon-info {
    display: block;
    background-color: rgb(20, 59, 115);
  }
  </style>
  