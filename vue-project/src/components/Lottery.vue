<script setup>
import { ref, onMounted, watch } from "vue";

const store = ref({
  value: "",
  status: 0,
  validate: () => {
    const value = store.value.value.toLowerCase();
    const options = document.querySelectorAll("#storeList option");

    let isValid = false;
    options.forEach((option) => {
      if (option.value.toLowerCase() === value) {
        isValid = true;
      }
    });
    if (store.value.value.length === 0) {
      store.value.status = 1;
      // console.log(store.value.status, store.value.value);
      return;
    } else if (!isValid) {
      store.value.status = 2;
      // console.log(store.value.status, store.value.value);
      return;
    } else {
      store.value.status = 3;
      // console.log(store.value.status, store.value.value);
      return;
    }
  },
});
const name = ref({
  value: "",
  status: 0,
  validate: () => {
    const pattern = new RegExp("^[\u4e00-\u9fa5a-zA-Z]+$");
    const isValid = pattern.test(name.value.value);
    if (name.value.value.length === 0) {
      name.value.status = 1;
      // console.log(name.value.status, name.value.value);
      return;
    } else if (!isValid) {
      name.value.status = 2;
      // console.log(name.value.status, isValid);
      return;
    } else {
      name.value.status = 3;
      // console.log(name.value.status, name.value.value);
      return;
    }
  },
});
const phone = ref({
  value: "",
  status: 0,
  validate: () => {
    const pattern = new RegExp("^09[-]?[\\d]{2}[-]?[\\d]{3}[-]?[\\d]{3}$");
    const isValid = pattern.test(phone.value.value);
    if (phone.value.value.length === 0) {
      phone.value.status = 1;
      // console.log(phone.value.status, phone.value.value);
      return;
    } else if (!isValid) {
      phone.value.status = 2;
      // console.log(phone.value.status, isValid, phone.value.value);
      return;
    } else {
      phone.value.status = 3;
      // console.log(phone.value.status, phone.value.value);
      return;
    }
  },
});
const consumption = ref({
  value: "",
  status: 0,
  validate: () => {
    if (consumption.value.value.length === 0) {
      consumption.value.status = 1;
      // console.log(consumption.value.status, consumption.value.value);
      return;
    } else if (!(parseInt(consumption.value.value) > 0)) {
      consumption.value.status = 2;
      // console.log(consumption.value.status);
      return;
    } else {
      consumption.value.status = 3;
      // console.log(consumption.value.status, consumption.value.value > 0);
      return;
    }
  },
});

const payment = ref("digital payment");

const submitText = ref("submit");
const submitStatus = ref(0);
function checkSubmit(arr) {
  if (arr.every((num) => num === 3)) {
    return 1;
  } else {
    return 2;
  }
}
function submit() {
  const inputStatusArray = [
    store.value.status,
    name.value.status,
    phone.value.status,
    consumption.value.status,
  ];
  submitStatus.value = checkSubmit(inputStatusArray);

  setTimeout(() => {
    submitStatus.value = 0;
  }, 3000);
  // console.log(inputStatusArray, 123, submitStatus.value);
}
</script>
<style lang="scss" scoped>
.lottery {
  padding: 24px 24px 58px;
  background-color: #e2d9d3;
  height: 797px;
  &__form {
    position: relative;
    padding-top: 43px;
    margin-bottom: 40px;
  }
  &__title-content {
    // pa
    position: absolute;
    top: 19px;
    left: 0;
    right: 0;
    margin: 0 auto;
    width: 163px;
    transform: translate(0.5px, 0px);
    p {
      width: 123px;
      padding: 10px 20px;
      border-radius: 50px;
      border: 2px solid var(--primary-color-2, #b57556);
      background: var(--text-color-white, #fff);
      box-shadow: 0px 1px 10px 0px rgba(73, 72, 72, 0.25);
      color: var(--primary-color-2, #b57556);
      text-align: center;
      font-family: Noto Sans TC;
      font-size: 18px;
      font-style: normal;
      font-weight: 700;
      line-height: 125%;
      // letter-spacing: 3.6px;
      margin: 0;
      display: inline-block;
    }
  }
  &__turtle {
    position: absolute;
    right: 0;
    top: -10px;
  }
  &__input {
    margin-top: 4px;
    width: 100%;
    height: 57px;
    padding: 7px 15px;
    border-radius: 20px;
    border: 1px solid var(--primary-color-1, #204379);
    background: var(--text-color-white, #fff);

    color: var(--text-color-text-color-2, #212121);
    /* Body 16px R */
    font-family: Noto Sans TC;
    font-size: 16px;
    font-style: normal;
    font-weight: 400;
    line-height: 140%;
    overflow: hidden;

    &--hidden {
      background: url("../assets/icons.png") no-repeat right 15px center;
    }
    &#payment {
      -webkit-appearance: none;
      -moz-appearance: none;
      appearance: none;
      background: url("../assets/icons.png") no-repeat right 15px center;
    }
    input {
      border: 0;
      height: 100%;
      width: 120%;
      outline: none;

      color: var(--text-color-text-color-2, #212121);
      font-family: Noto Sans TC;
      font-size: 16px;
      font-style: normal;
      font-weight: 400;
      line-height: 140%;
      background-color: transparent;
      &::placeholder {
        color: var(--text-color-text-color-7, #bdbdbd);
        /* Body 16px R */
        font-family: Noto Sans TC;
        font-size: 16px;
        font-style: normal;
        font-weight: 400;
        line-height: 140%;
      }
    }
    &:hover {
      -webkit-appearance: none;
      -moz-appearance: none;
      appearance: none;
    }
    &:focus {
      -webkit-appearance: none;
      -moz-appearance: none;
      appearance: none;
      outline: none; /* 取消聚焦時的默認外框線 */
      padding: 5px 13px;
      border-radius: 20px;
      border: 3px solid #93bbf9;
      background: var(--text-color-white, #fff);
    }
    &:focus-within {
      -webkit-appearance: none;
      -moz-appearance: none;
      appearance: none;
      outline: none; /* 取消聚焦時的默認外框線 */
      padding: 5px 13px;
      border-radius: 20px;
      border: 3px solid #93bbf9;
      // background: var(--text-color-white, #fff);
    }
    &::placeholder {
      color: var(--text-color-text-color-7, #bdbdbd);
      /* Body 16px R */
      font-family: Noto Sans TC;
      font-size: 16px;
      font-style: normal;
      font-weight: 400;
      line-height: 140%;
    }
    &-group {
      border-radius: 16px;
      border: 2px solid var(--primary-color-2, #b57556);
      background: #fff;
      box-shadow: 0px 1px 20px 0px rgba(73, 72, 72, 0.25);
      max-width: 808px;
      margin: 0 auto;
      padding: 38px 18px;
      flex-direction: column;
      align-items: center;
      gap: 20px;
      height: 575px;
      padding: 40px 20px;

      label {
        display: block;
        color: var(--primary-color-1, #204379);
        /* Body 16px R */
        font-family: Noto Sans TC;
        font-size: 16px;
        font-style: normal;
        font-weight: 400;
        line-height: 140%;
        position: relative;
        padding-bottom: 4px;
        &.error {
          .lottery__input {
            border-radius: 20px;
            padding: 5px 13px;
            border: 3px solid #e06d6d;
            background: var(--text-color-white, #fff);
          }
          &::before {
            content: "wrong format";
            color: #e06d6d;
            position: absolute;
            top: 100%;
            left: 0px;
            /* Capation 12px R */
            font-family: Noto Sans TC;
            font-size: 12px;
            font-style: normal;
            font-weight: 400;
            line-height: 140%;
            order: 99;
          }
        }
        &.no-result {
          .lottery__input {
            border-radius: 20px;
            padding: 5px 13px;
            border: 3px solid #e06d6d;
            background: var(--text-color-white, #fff);
          }
          &::before {
            content: "no result";
            color: #e06d6d;
            position: absolute;
            top: 100%;
            left: 0px;
            /* Capation 12px R */
            font-family: Noto Sans TC;
            font-size: 12px;
            font-style: normal;
            font-weight: 400;
            line-height: 140%;
            order: 99;
          }
        }
        &.required {
          .lottery__input {
            border-radius: 20px;
            padding: 5px 13px;
            border: 3px solid #e06d6d;
            background: var(--text-color-white, #fff);
          }
          &::before {
            content: "required";
            color: #e06d6d;
            position: absolute;
            top: 100%;
            left: 0px;
            /* Capation 12px R */
            font-family: Noto Sans TC;
            font-size: 12px;
            font-style: normal;
            font-weight: 400;
            line-height: 140%;
            order: 99;
          }
        }
        span {
          margin-left: 4px;
          color: var(--primary-color-2, #b57556);
          /* Subtitle 14px B */
          font-family: Noto Sans TC;
          font-size: 14px;
          font-style: normal;
          font-weight: 700;
          line-height: 140%;
        }
        + label {
          margin-top: 16px;
        }
      }
    }
  }
  &__submit {
    width: 200px;
    margin: 0 auto;
    height: 57px;
    border-radius: 50px;
    background: var(--primary-color-2, #b57556);
    box-shadow: 0px -4px 10px 0px rgba(255, 255, 255, 0.9),
      0px 4px 10px 0px rgba(40, 35, 35, 0.35);
    color: var(--text-color-white, #fff);
    padding: 16px 20px;
    font-family: Noto Sans TC;
    font-size: 18px;
    font-style: normal;
    font-weight: 700;
    line-height: 125%;
    letter-spacing: 3.6px;
    text-align: center;
    transition: all 1s ease;

    border: 0;
    display: block;
    cursor: pointer;
    &:hover {
      transform: scale(1.05);
    }
    &:active {
      border-radius: 50px;
      background: #d3a995;
      box-shadow: 0px -4px 10px 0px rgba(255, 255, 255, 0.9),
        0px 4px 10px 0px rgba(40, 35, 35, 0.35);
    }
    &--pass {
      display: flex;
      justify-content: center;
      color: #e6ffb1;
      font-family: Noto Sans TC;
      font-size: 18px;
      font-style: normal;
      font-weight: 700;
      line-height: 125%;
      letter-spacing: 3.6px;
      pointer-events: none;
      cursor: none;
    }
    &--failure {
      display: flex;
      justify-content: center;
      color: #ffe3e3;
      font-family: Noto Sans TC;
      font-size: 18px;
      font-style: normal;
      font-weight: 700;
      line-height: 125%;
      letter-spacing: 3.6px;
      pointer-events: none;
      cursor: none;
    }
    svg {
      margin-right: 16px;
    }
  }
}
@media screen and (min-width: 768px) {
}
@media screen and (min-width: 1400px) {
}
</style>
<template>
  <form class="lottery" id="form" @submit.prevent="submit()">
    <div class="lottery__form">
      <fieldset class="lottery__input-group">
        <legend class="lottery__title-content">
          <p>ＦＯＲＭ</p>
          <svg
            class="lottery__turtle"
            width="65"
            height="62"
            viewBox="0 0 65 62"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M54.1362 49.89C55.6839 50.1319 57.3518 49.5346 58.3576 48.4046C57.9278 49.1956 53.895 46.4196 53.2329 45.887C52.3794 45.2172 51.9106 44.0712 50.7005 44.4183C49.9332 44.6201 49.2239 45.1529 48.8091 45.8389C48.2461 46.8236 48.6137 47.2028 49.4822 47.7677C50.7914 48.9379 52.4853 49.6318 54.1362 49.89Z"
              fill="#9BB554"
            />
            <path
              d="M19.8381 11.4222C20.497 8.29669 20.6216 5.94856 18.1457 3.30104C15.0212 0.0139061 5.9785 -1.07849 7.23123 5.6824C7.72711 8.12766 9.70304 9.83596 11.0283 11.6577C12.2502 13.4632 12.8796 15.7142 13.5392 17.7545C14.3453 20.2484 14.4577 22.4183 16.4035 24.3372C17.6123 25.4949 19.3965 27.0656 21.1717 26.4825C25.4913 25.1138 19.8437 20.2479 19.1992 18.1023C18.4512 15.9404 19.33 13.495 19.8381 11.4222Z"
              fill="#9BB554"
            />
            <path
              d="M27.6271 31.5107C25.2674 28.7726 20.7386 29.3563 19.1474 32.3377C17.6015 35.0033 17.7832 38.9082 18.6333 41.8409C19.4101 44.5467 23.5414 54.1305 27.6301 52.1858C31.1408 50.5814 26.5057 46.7336 25.9188 44.9189C25.0536 42.0915 25.4307 39.4585 27.1082 37.352C28.6521 35.4399 29.5447 33.6413 27.6271 31.5107Z"
              fill="#9BB554"
            />
            <path
              d="M46.2396 42.5674C44.3372 40.3315 40.5633 40.8179 39.1662 43.1836C37.9028 45.3549 38.0715 48.6116 38.7899 50.9853C39.42 53.2374 42.8457 61.0955 46.2377 59.5803C49.0669 58.3001 45.3033 55.0193 44.8782 53.553C44.1447 51.2846 44.4765 48.9676 45.8715 47.3553C47.1329 45.9375 47.7732 44.4225 46.2396 42.5674Z"
              fill="#9BB554"
            />
            <path
              d="M54.0978 39.6789C55.8165 42.4179 57.2987 45.3348 54.0322 47.5087C50.5141 49.9653 45.6642 48.4547 42.3047 46.8551C34.0824 43.0984 25.3438 39.2609 20.6607 30.6881C18.8989 27.5127 17.4488 23.6342 17.6805 19.8042C17.9273 15.869 20.7255 17.7031 23.3816 17.5816C24.5472 17.5492 25.6827 17.7269 26.8484 17.6945C28.2355 17.5893 29.4012 17.5569 30.7281 17.872C34.7091 18.817 37.6967 21.5399 40.7875 24.2788C45.9239 28.9489 53.4195 34.0954 54.7131 41.2787"
              fill="#738841"
            />
            <path
              d="M32.0967 37.8284C36.4405 41.4093 41.6856 44.594 47.2316 45.6768C52.7775 46.7596 55.4746 42.6689 55.6653 37.6487C55.7316 34.9728 54.6901 32.6609 53.3388 30.3005C49.9757 24.2943 44.3688 18.4742 37.689 16.4618C31.9235 14.6999 19.8749 17.0049 21.4766 24.9918C22.568 30.6424 27.8411 34.3687 32.0967 37.8284Z"
              fill="#9BB554"
            />
            <path
              d="M32.4026 16.7883C32.5058 16.8045 32.5058 16.8045 32.4026 16.7883C34.4241 16.675 36.3122 16.7557 37.7273 17.1919C38.994 17.927 40.2307 18.8721 41.0094 20.0678C41.3621 20.5526 41.5966 21.1262 41.4031 21.7402C41.1946 22.4593 40.5883 23.0087 39.9088 23.332C39.6722 23.5097 39.4508 23.5825 39.126 23.639C38.8013 23.6956 38.3583 23.8411 38.1519 23.8088C38.0486 23.7926 38.0487 23.7926 37.9304 23.8815C37.3992 23.9058 36.8681 23.9301 36.3519 23.8493C35.3197 23.6878 33.9777 23.4779 33.2422 22.7185C32.1538 21.4743 29.8329 17.7823 32.4026 16.7883Z"
              fill="#C1CC64"
            />
            <path
              d="M41.9702 23.4259C42.431 22.4222 42.4782 21.3537 42.3187 20.2529C42.674 19.9858 42.9992 19.9291 43.4126 19.9938C44.9461 21.0945 46.3612 22.2843 47.6578 23.5631C47.996 24.1539 48.2008 24.9391 48.1104 25.5704C47.8564 26.6065 46.657 27.6022 45.6815 27.7723C44.3807 27.999 43.2155 27.2787 42.5241 26.2022C42.1859 25.6114 41.9812 24.8262 41.8648 24.1625C41.8949 23.9521 41.9251 23.7416 41.9702 23.4259C41.9552 23.5311 41.9552 23.5311 41.9702 23.4259Z"
              fill="#C1CC64"
            />
            <path
              d="M46.1461 44.0292C45.0993 43.9728 43.9945 43.5855 42.9778 43.3193C42.477 43.1338 40.0159 42.6418 39.7084 41.843C39.8266 41.7542 39.9448 41.6654 40.048 41.6815C40.048 41.6815 40.1512 41.6977 40.1662 41.5928C41.3161 41.6653 42.4961 41.528 43.4847 41.2536C44.1489 41.0357 44.813 40.8178 45.404 40.3739C45.3869 41.2293 45.473 42.1007 45.9869 42.9318C46.2513 43.2949 46.4125 43.6418 46.7952 43.9162C46.6769 44.0049 46.4556 44.0776 46.1461 44.0292Z"
              fill="#C1CC64"
            />
            <path
              d="M42.6894 40.3614C42.5861 40.3452 42.4829 40.3291 42.3796 40.3129C41.6416 40.3049 40.9768 40.5233 40.2388 40.5152C39.3975 40.491 38.5713 40.3618 37.7902 39.9171C37.0973 39.5937 36.3313 39.0438 35.7567 38.6315C35.2855 38.2353 35.3026 37.3782 35.3778 36.8526C35.3798 36.1006 35.7498 35.7285 36.0617 35.025C36.522 34.0223 37.4987 33.1004 38.4303 32.4939C39.9234 31.6528 42.3179 30.4154 43.9533 31.5311C44.0265 31.7576 44.1147 31.8788 44.2912 32.1214C44.9519 33.4071 46.129 34.7735 47.5449 35.2101C46.5682 36.132 45.9595 37.4339 45.6606 38.7844C45.5573 38.7682 45.439 38.8571 45.4089 39.0674C45.125 40.3127 43.8556 40.329 42.6894 40.3614Z"
              fill="#C1CC64"
            />
            <path
              d="M27.3403 29.8081C27.8894 28.9256 28.5269 28.1646 29.3711 27.436C30.2154 26.7073 31.0295 26.1892 32.0503 25.7034C32.5091 25.4524 33.1014 25.0071 33.4396 25.598C33.7046 25.9623 33.5259 26.4723 33.5841 26.8042C33.6704 27.6785 33.7717 28.4475 34.0799 29.249C34.2997 29.929 34.5345 30.5037 34.8728 31.0946C35.211 31.6856 35.6828 32.0822 36.021 32.6732C36.5359 33.5069 35.7951 34.2517 35.3795 34.9399C34.9639 35.628 34.5482 36.3162 34.221 37.1257C33.4068 37.6439 31.1815 35.4664 30.7098 35.0698C30.0613 34.4303 29.2794 33.9851 28.5126 33.4347C27.7607 32.779 26.8172 31.9858 26.8645 30.9172L26.8795 30.8119C26.9398 30.391 27.0883 30.0914 27.3403 29.8081Z"
              fill="#C1CC64"
            />
            <path
              d="M30.144 17.1102C30.3357 17.2478 30.5275 17.3854 30.6007 17.6121C30.2282 18.7376 30.7412 20.3244 31.3294 21.385C31.5944 21.7493 31.7561 22.0974 32.1245 22.4779C32.1245 22.4779 32.1245 22.4779 32.1094 22.5831C32.0944 22.6884 32.1978 22.7046 32.2861 22.826C32.2711 22.9313 32.3745 22.9474 32.3594 23.0527C32.4477 23.1741 32.5361 23.2956 32.6244 23.417C32.8011 23.6599 32.771 23.8704 32.6224 24.17C32.5039 24.259 32.4888 24.3643 32.5772 24.4857C32.3402 24.6639 31.9999 24.8258 31.778 24.8987C30.7419 25.4898 29.6174 25.9595 28.758 26.7935C28.1506 27.3441 27.6466 27.9109 27.1275 28.5829C27.0241 28.5667 27.009 28.672 27.009 28.672C26.6235 29.1497 25.9407 30.2265 25.1888 29.5708C24.6286 29.0527 24.3054 28.3564 23.9671 27.7654C23.4521 26.9315 22.8337 26.0815 22.4372 25.1585C22.3488 25.0371 22.379 24.8266 22.2906 24.7051C21.9626 20.3494 25.9002 17.9526 30.144 17.1102Z"
              fill="#C1CC64"
            />
            <path
              d="M34.9843 24.3066C35.3975 24.3713 35.9139 24.4521 36.3271 24.5168C36.9469 24.6138 37.685 24.6218 38.3348 24.5085L38.4381 24.5247C38.763 24.4681 39.1913 24.4276 39.5312 24.2658C40.1811 24.1525 40.9342 24.0554 40.9924 24.387C40.9773 24.4921 41.0656 24.6135 41.1689 24.6296C41.2701 25.398 41.5779 26.1986 42.0192 26.8051C42.3721 27.2904 42.7402 27.6705 43.2266 27.9616C43.388 28.3093 43.5645 28.552 43.6076 28.9887C43.4441 29.3931 43.3839 29.8137 42.9406 29.9593C42.8223 30.0483 42.719 30.0321 42.7039 30.1372C41.0212 30.0888 39.2029 30.9867 37.9313 31.7551C37.6946 31.9331 37.4579 32.111 37.2363 32.1838C35.7902 31.9575 35.0281 29.9033 34.5589 28.7549C34.2962 27.6388 33.7708 25.4066 34.9843 24.3066Z"
              fill="#C1CC64"
            />
            <path
              d="M48.2891 35.6241C48.4076 35.535 48.4077 35.535 48.4227 35.4297C49.6792 35.5187 51.0111 35.0813 51.9593 34.3685L52.0778 34.2794C52.4334 34.0121 52.9075 33.6557 53.2781 33.2831C53.5001 33.2102 53.707 33.2426 54.0023 33.3965C54.4573 34.6517 54.7053 35.8746 54.7162 37.2757C54.6519 39.2032 54.1887 40.9607 53.2536 42.3214C53.0316 42.3943 52.898 42.5886 52.7794 42.6777C52.6609 42.7668 52.6459 42.8721 52.6308 42.9774C52.1416 43.4391 51.6524 43.9007 50.9865 44.1195C49.9951 44.3949 49.0942 44.0386 48.0597 43.8767L47.9562 43.8605C47.5725 43.5852 47.2039 43.2046 46.9539 42.7349C46.2619 41.6578 46.3092 40.5888 46.5784 39.4468C46.6859 37.9566 47.2957 36.6527 48.2891 35.6241Z"
              fill="#C1CC64"
            />
            <path
              d="M44.6404 29.6551C44.6856 29.3395 44.7609 28.8136 45.1893 28.7731C45.2926 28.7893 45.3076 28.6841 45.411 28.7003C45.5143 28.7165 45.6327 28.6275 45.736 28.6436C46.7112 28.4736 47.8649 27.7939 48.4137 26.9119C48.4137 26.9119 48.4137 26.9119 48.4287 26.8067C48.6956 26.4184 49.0658 26.0461 49.6557 26.3535C49.759 26.3697 49.759 26.3697 49.8623 26.3859C50.2305 26.7661 50.4803 27.2354 50.7451 27.5995C51.2747 28.3276 51.8044 29.0558 52.2307 29.7678C52.6571 30.4798 52.965 31.2807 52.5346 32.0737C52.5195 32.1789 52.5045 32.2841 52.4894 32.3892C52.3259 32.7938 52.0741 33.077 51.8222 33.3602C51.5855 33.5382 51.3487 33.7163 51.127 33.7891C51.0086 33.8781 51.0086 33.8781 50.9936 33.9833C49.9582 34.574 48.5397 34.8897 47.375 34.1697C46.2103 33.4497 45.0326 32.0824 44.6966 30.7393C44.6384 30.4076 44.5803 30.0758 44.5221 29.7441C44.507 29.8493 44.6254 29.7603 44.6404 29.6551Z"
              fill="#C1CC64"
            />
            <path
              d="M20.6818 33.0042C20.8584 33.247 21.0351 33.4899 21.0933 33.8217C21.0632 34.0322 20.9297 34.2265 20.7078 34.2994C20.486 34.3723 20.2792 34.3399 20.1909 34.2185C19.9992 34.0809 19.8225 33.838 19.956 33.6437C19.9861 33.4333 20.1197 33.239 20.2381 33.1499C20.3566 33.0609 20.4599 33.077 20.5633 33.0932C20.6517 33.2146 20.8585 33.247 20.8283 33.4575L20.8133 33.5627C20.8133 33.5627 20.7982 33.668 20.8133 33.5627C20.9016 33.6842 20.8715 33.8946 20.753 33.9837C20.6346 34.0727 20.4278 34.0404 20.3394 33.919C20.2511 33.7975 20.2662 33.6923 20.2813 33.587C20.2813 33.587 20.2813 33.5871 20.2963 33.4818C20.2813 33.5871 20.2813 33.587 20.2813 33.587C20.3847 33.6032 20.5031 33.5142 20.6065 33.5304C20.6065 33.5304 20.488 33.6194 20.473 33.7247C20.488 33.6194 20.473 33.7247 20.473 33.7247C20.473 33.7247 20.473 33.7247 20.4579 33.8299C20.4428 33.9351 20.473 33.7247 20.4579 33.8299C20.4579 33.8299 20.4579 33.8299 20.4428 33.9351C20.4579 33.8299 20.4428 33.9351 20.4428 33.9351C20.4428 33.9351 20.4579 33.8299 20.4428 33.9351C20.4428 33.9351 20.3545 33.8137 20.4428 33.9351C20.4428 33.9351 20.3545 33.8137 20.4428 33.9351C20.4428 33.9351 20.3394 33.919 20.4428 33.9351C20.4428 33.9351 20.3394 33.919 20.4428 33.9351C20.5462 33.9513 20.3394 33.919 20.4428 33.9351C20.4428 33.9351 20.3394 33.919 20.4428 33.9351C20.5462 33.9513 20.3394 33.919 20.4428 33.9351C20.3244 34.0242 20.4428 33.9351 20.4428 33.9351C20.4579 33.8299 20.4278 34.0404 20.4428 33.9351C20.4579 33.8299 20.4278 34.0404 20.4428 33.9351C20.4278 34.0404 20.4428 33.9351 20.4428 33.9351C20.4579 33.8299 20.4278 34.0404 20.4428 33.9351C20.4428 33.9351 20.4428 33.9351 20.4579 33.8299C20.4579 33.8299 20.473 33.7247 20.4579 33.8299C20.4579 33.8299 20.4579 33.8299 20.3696 33.7085C20.3696 33.7085 20.3696 33.7085 20.2813 33.587C20.1929 33.4656 20.1046 33.3442 20.2381 33.1499C20.3867 32.8504 20.5935 32.8828 20.6818 33.0042Z"
              fill="#738841"
            />
            <path
              d="M21.2722 35.474C21.2872 35.3688 21.2722 35.474 21.2722 35.474C21.2872 35.3688 21.2722 35.474 21.2722 35.474C21.4638 35.6116 21.5522 35.733 21.5371 35.8382C21.507 36.0487 21.2701 36.2267 21.0784 36.0892C20.9751 36.073 20.8868 35.9516 20.7985 35.8302C20.7102 35.7088 20.6068 35.6926 20.6369 35.4822C20.652 35.3769 20.667 35.2717 20.7855 35.1827C20.9189 34.9884 21.229 35.037 21.4207 35.1746C21.5241 35.1907 21.5973 35.4173 21.5823 35.5226C21.5672 35.6278 21.3454 35.7006 21.1387 35.6683C21.1387 35.6683 21.242 35.6845 21.1387 35.6683C21.1387 35.6683 21.0353 35.6521 21.1387 35.6683C21.1387 35.6683 21.0353 35.6521 21.1387 35.6683C21.1387 35.6683 21.1387 35.6683 21.242 35.6845C21.242 35.6845 21.2571 35.5792 21.242 35.6845C21.2571 35.5792 21.1688 35.4578 21.1688 35.4578C21.0654 35.4417 21.1688 35.4578 21.2722 35.474C21.2722 35.474 21.1688 35.4578 21.2722 35.474C21.2571 35.5792 21.3605 35.5954 21.3605 35.5954C21.242 35.6845 21.1236 35.7735 20.9018 35.8464C20.8868 35.9516 20.9018 35.8464 20.9018 35.8464C20.9018 35.8464 20.7985 35.8302 20.8135 35.725C20.7252 35.6036 20.6369 35.4822 20.652 35.3769C20.667 35.2717 20.8005 35.0775 20.9039 35.0937C21.1106 35.126 21.3023 35.2636 21.2722 35.474Z"
              fill="#738841"
            />
            <path
              d="M19.9814 34.9462C19.9664 35.0515 20.0397 35.2783 19.9211 35.3674C19.906 35.4727 19.8025 35.4566 19.7875 35.5619C19.6689 35.651 19.477 35.5133 19.492 35.408C19.4036 35.2865 19.4187 35.1811 19.4338 35.0758C19.4488 34.9705 19.5825 34.7761 19.686 34.7923C19.7895 34.8085 19.893 34.8247 19.893 34.8247C19.9965 34.8409 19.9814 34.9462 19.9664 35.0515C19.9513 35.1568 19.9814 34.9462 19.9664 35.0515C19.9814 34.9462 19.8779 34.93 19.8779 34.93L19.7744 34.9138C19.7744 34.9138 19.6709 34.8976 19.6558 35.0029C19.5523 34.9867 19.5373 35.092 19.5222 35.1973C19.5222 35.1973 19.5373 35.092 19.5222 35.1973C19.5373 35.092 19.5373 35.0921 19.5524 34.9867C19.5674 34.8814 19.7011 34.687 19.8046 34.7032C19.8197 34.5979 20.0116 34.7356 19.9814 34.9462Z"
              fill="#738841"
            />
            <path
              d="M41.4014 51.9409C41.4746 52.1675 41.5629 52.2889 41.5328 52.4993C41.591 52.8311 41.1474 52.9769 40.9708 52.7341C40.7942 52.4913 40.721 52.2647 40.6478 52.0381C40.4862 51.6901 41.0331 51.5606 41.1947 51.9086C41.2679 52.1352 41.3411 52.3618 41.4294 52.4832C41.2077 52.556 41.0893 52.6451 40.8675 52.7179C40.7942 52.4913 40.706 52.3699 40.7361 52.1595C40.693 51.7225 41.2398 51.5929 41.4014 51.9409Z"
              fill="#738841"
            />
            <path
              d="M40.4463 52.0126C40.4313 52.1179 40.4162 52.2233 40.4011 52.3286C40.386 52.4339 40.2524 52.6284 40.1488 52.6122C40.0453 52.596 39.8534 52.4582 39.8684 52.3529C39.8835 52.2476 39.8986 52.1423 39.9137 52.037C39.9288 51.9317 40.0625 51.7372 40.166 51.7534C40.2846 51.6643 40.4765 51.802 40.4463 52.0126Z"
              fill="#738841"
            />
            <path
              d="M41.0155 53.18C41.0004 53.2853 41.0888 53.4067 41.0737 53.512C41.1621 53.6335 41.0285 53.8278 40.91 53.9169C40.7915 54.006 40.5997 53.8683 40.5114 53.7469C40.5264 53.6416 40.4381 53.5201 40.4531 53.4149C40.3648 53.2934 40.4983 53.0991 40.6168 53.01C40.8388 52.9371 40.9422 52.9533 41.0155 53.18Z"
              fill="#738841"
            />
            <path
              d="M19.0852 7.83127C19.1736 7.95271 19.2619 8.07414 19.2469 8.17939C19.2167 8.38991 18.8914 8.44662 18.6997 8.30899C18.5079 8.17137 18.4497 7.8394 18.4798 7.62889C18.4949 7.52364 18.5099 7.41839 18.6284 7.32932C18.7469 7.24025 18.8352 7.36166 18.9236 7.4831C19.027 7.49929 19.1154 7.62075 19.0852 7.83127C19.2037 7.74219 19.2037 7.74219 19.0852 7.83127C19.1886 7.84745 19.1886 7.84745 19.0852 7.83127C19.1886 7.84745 19.1736 7.95271 19.1736 7.95271C19.2619 8.07416 19.2318 8.28466 19.1133 8.37373C18.9948 8.4628 18.788 8.43044 18.6997 8.30899C18.6113 8.18755 18.6264 8.08228 18.523 8.0661L18.538 7.96083C18.538 7.96083 18.5531 7.85558 18.538 7.96083C18.7599 7.88795 18.8784 7.7989 19.0852 7.83127C19.0852 7.83127 19.0852 7.83127 19.0702 7.93653C19.1154 7.62076 19.1003 7.72601 19.0852 7.83127C19.1003 7.72601 19.1003 7.72601 19.0852 7.83127C19.1886 7.84745 19.0852 7.83127 19.0852 7.83127C19.1886 7.84745 19.0852 7.83127 19.0852 7.83127C19.0852 7.83127 19.1736 7.95271 19.0852 7.83127C19.0852 7.83127 19.1886 7.84745 19.0852 7.83127C18.9818 7.81508 18.9818 7.81508 18.8784 7.79889C18.775 7.78271 18.7599 7.88797 18.6565 7.87179C18.6415 7.97705 18.6415 7.97703 18.6264 8.08228C18.6264 8.08228 18.6113 8.18755 18.7147 8.20373C18.6264 8.08229 18.5531 7.8556 18.6716 7.76653C18.7901 7.67745 18.9969 7.70982 19.0852 7.83127Z"
              fill="#738841"
            />
            <path
              d="M18.8669 9.31478C18.7335 9.50904 18.7335 9.50904 18.8669 9.31478C18.6602 9.28242 18.4535 9.25007 18.2317 9.32293L18.2467 9.2177C18.4535 9.25006 18.6602 9.28242 18.8669 9.31478C18.7485 9.40382 18.7485 9.40382 18.8669 9.31478C18.6 9.70331 18.1132 9.41196 18.3652 9.12865C18.4103 8.81298 18.8088 8.98293 18.8669 9.31478C18.8519 9.42 18.8368 9.52524 18.8368 9.52524C18.6883 9.82472 18.3932 9.67096 18.32 9.44434C18.2317 9.32294 18.3501 9.23387 18.3652 9.12865C18.307 8.7968 18.9121 8.99911 18.8669 9.31478Z"
              fill="#738841"
            />
            <path
              d="M17.9114 8.62566C18.0148 8.64185 18.1183 8.65805 18.1183 8.65805C18.1334 8.55275 18.1183 8.65805 18.1183 8.65805C18.1334 8.55275 18.1183 8.65805 18.1183 8.65805C18.1032 8.76334 17.9696 8.95773 17.8661 8.94154C17.7627 8.92535 17.5708 8.78769 17.5859 8.68239C17.601 8.5771 17.6311 8.36651 17.6462 8.26122C17.6613 8.15592 17.7647 8.1721 17.7798 8.0668C17.8983 7.9777 18.0018 7.99388 18.1053 8.01008C18.2088 8.02627 18.2821 8.25306 18.267 8.35836C18.2218 8.67425 18.1032 8.76334 17.9114 8.62566Z"
              fill="#738841"
            />
            <ellipse
              cx="1.05319"
              cy="1.05786"
              rx="1.05319"
              ry="1.05786"
              transform="matrix(0.99761 -0.0430195 0.0498394 1.00022 13.3984 3.60547)"
              fill="#6C6C6C"
            />
          </svg>
        </legend>
        <label
          id="store"
          for="store"
          :class="{
            required: store.status === 1,
            'no-result': store.status === 2,
          }"
          >store<span>*</span>
          <div class="lottery__input lottery__input--hidden">
            <input
              type="text"
              name="store"
              id="store"
              list="storeList"
              placeholder="Please enter the store."
              v-model.lazy="store.value"
              @blur="store.validate()"
              required
            />
            <datalist id="storeList">
              <option value="store1"></option>
              <option value="store2"></option>
              <option value="store3"></option>
              <option value="store4"></option>
              <option value="store5"></option>
              <option value="store6"></option>
            </datalist>
          </div>
        </label>
        <label
          id="name"
          for="name"
          :class="{
            required: name.status === 1,
            error: name.status === 2,
          }"
          >name<span>*</span>
          <input
            class="lottery__input"
            type="text"
            name="name"
            id="name"
            placeholder="Please enter your name."
            v-model.lazy="name.value"
            @blur="name.validate()"
            required
          />
        </label>
        <label
          id="phone"
          for="phone"
          :class="{
            required: phone.status === 1,
            error: phone.status === 2,
          }"
          >phone<span>*</span>
          <input
            class="lottery__input"
            type="tel"
            inputmode="tel"
            name="phone"
            id="phone"
            placeholder="Please enter your phone number."
            v-model.lazy="phone.value"
            @blur="phone.validate()"
            required
          />
        </label>
        <label
          id="consumption"
          for="consumption"
          :class="{
            required: consumption.status === 1,
            error: consumption.status === 2,
          }"
          >Amount of consumption<span>*</span>
          <input
            class="lottery__input"
            type="number"
            inputmode="numeric"
            name="consumption"
            id="consumption"
            placeholder="Please enter your consumption."
            v-model.lazy="consumption.value"
            @blur="consumption.validate()"
            required
          />
        </label>
        <label id="payment" for="payment"
          >payment<span>*</span>
          <select
            class="lottery__input"
            v-model.lazy="payment"
            name="payment"
            id="payment"
          >
            <option value="digital payment">digital payment</option>
            <option value="ATM">ATM</option>
          </select>
        </label>
      </fieldset>
    </div>
    <button v-if="submitStatus === 0" class="lottery__submit" type="submit">
      submit
    </button>
    <button
      v-else-if="submitStatus === 1"
      class="lottery__submit lottery__submit--pass"
      type="submit"
    >
      <svg
        width="24"
        height="25"
        viewBox="0 0 24 25"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          fill-rule="evenodd"
          clip-rule="evenodd"
          d="M12 0.5C5.376 0.5 0 5.876 0 12.5C0 19.124 5.376 24.5 12 24.5C18.624 24.5 24 19.124 24 12.5C24 5.876 18.624 0.5 12 0.5ZM9.35615 14.8608C9.49088 14.9952 9.70897 14.995 9.84351 14.8605L16.656 8.04801C17.1261 7.57794 17.8886 7.57929 18.357 8.05101C18.8231 8.52038 18.8217 9.27829 18.354 9.74601L10.4276 17.6724C9.97052 18.1295 9.22948 18.1295 8.77241 17.6724L4.44659 13.3466C3.97903 12.879 3.97903 12.121 4.44659 11.6534C4.91369 11.1863 5.67084 11.1858 6.13859 11.6522L9.35615 14.8608Z"
          fill="#E6FFB1"
        />
      </svg>

      success
    </button>
    <button
      v-else-if="submitStatus === 2"
      class="lottery__submit lottery__submit--failure"
      type="submit"
    >
      <svg
        width="24"
        height="25"
        viewBox="0 0 24 25"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          fill-rule="evenodd"
          clip-rule="evenodd"
          d="M20.4871 20.9853C18.2367 23.2357 15.1844 24.5 12.0018 24.5C8.81921 24.5 5.76697 23.2357 3.51653 20.9853C1.26609 18.7348 0.00181287 15.6826 0.00181287 12.5C0.00181287 9.3174 1.26609 6.26516 3.51653 4.01472C5.76697 1.76428 8.81921 0.5 12.0018 0.5C15.1844 0.5 18.2367 1.76428 20.4871 4.01472C22.7375 6.26516 24.0018 9.3174 24.0018 12.5C24.0018 15.6826 22.7375 18.7348 20.4871 20.9853ZM16.2445 8.25736C15.7758 7.78873 15.016 7.78873 14.5474 8.25736L12.0018 10.8029L9.45623 8.25736C8.9876 7.78873 8.2278 7.78873 7.75917 8.25736V8.25736C7.29054 8.72599 7.29054 9.48579 7.75917 9.95441L10.3048 12.5L7.75917 15.0456C7.29054 15.5142 7.29054 16.274 7.75917 16.7426V16.7426C8.2278 17.2113 8.9876 17.2113 9.45623 16.7426L12.0018 14.1971L14.5474 16.7426C15.016 17.2113 15.7758 17.2113 16.2445 16.7426V16.7426C16.7131 16.274 16.7131 15.5142 16.2445 15.0456L13.6989 12.5L16.2445 9.95442C16.7131 9.48579 16.7131 8.72599 16.2445 8.25736V8.25736Z"
          fill="#FFE3E3"
        />
      </svg>
      failure
    </button>
    <!-- <input class="lottery__submit" type="submit" :value="submitText" /> -->
  </form>
</template>
