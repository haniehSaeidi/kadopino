<template>
  <div class="mt-3">
    <div class="columns is-mobile">
      <div class="column is-full-mobile is-half-desktop is-half-tablet">
        <div class="group">
          <input type="text"
								 v-model="name"
								 :class="{ redBorder: isNameInvalid }" 
								 @input="nameValidation"
								 required 
					/> 
          <label :class="{ redColor: isNameInvalid }">
            <BaseIcon name="user" />نام و نام خانوادگی
          </label>
        </div>
      </div>
    </div>
    <div class="columns is-mobile">
      <div class="column is-full-mobile is-half-desktop is-half-tablet">
        <div class="group">
          <input type="text"
								 v-model="phoneNumber"
								 :class="{ redBorder: isPhoneNumberInvalid }"
								 required
								 @input="phoneNumberValidation"
          />
          <label :class="{ redColor: isPhoneNumberInvalid }">
            <BaseIcon name="phone" />شماره همراه
          </label>
        </div>
      </div>
    </div>
    <div class="columns is-mobile">
      <div class="column is-full-mobile is-half-desktop is-half-tablet">
        <div class="group">
          <input ref="pass"
								 autocomplete="new-password"
								 type="password"
								 v-model="password"
								 :class="{ redBorder: isPasswordInvalid }"
								 required
								 @input="passwordValidation"
          />
          <label :class="{ redColor: isPasswordInvalid }">
            <BaseIcon name="lock" />رمز عبور دلخواه
          </label>
          <p class="font-size-12">رمز عبور 6 حرف با حروف انگلیسی باشد.</p>
        </div>
      </div>
    </div>
    <div class="columns is-mobile">
      <div class="column is-full-mobile is-half-desktop is-half-tablet">
        <button class="button success-btn width-100"
								@click="submit"
								:disabled="isDisableBtn"
								:class="[isDisableBtn ? 'disableBtn' : 'ableBtn']"
        >ثبت نام</button>
        <div class="text-center mt-1">
          <span>قبلا ثبت نام کرده اید؟</span>
          <span class="bold">ورود</span>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import BaseIcon from "@/components/BaseIcon";

export default {
  components: {
    BaseIcon
  },
  data() {
    return {
      name: "",
      phoneNumber: "",
      password: "",
      isNameInvalid: false,
      isPhoneNumberInvalid: false,
      isPasswordInvalid: false,
      isDisableBtn: true
    };
  },
  methods: {
    submit() {
			if (
				!this.isNameInvalid &&
				!this.isPhoneNumberInvalid &&
				!this.isPasswordInvalid
			) {
				this.name = "";
				this.phoneNumber = "";
				this.password = "";
				this.isDisableBtn = true
			}
    },
    nameValidation(e) {
      if (e.target.value.length > 0) {
				this.isNameInvalid = false;
      } else {
				this.isNameInvalid = true
				this.isDisableBtn = true
			}
			this.checkingBtnIsDisabled()
		
    },
		phoneNumberValidation(e) {
      let regex = new RegExp("^(\\+98|0)?9\\d{9}$");
			let isValid = regex.test(e.target.value);
			isValid ?this.isPhoneNumberInvalid = false: this.isPhoneNumberInvalid = true; this.isDisableBtn = true
			this.checkingBtnIsDisabled()
    },
    passwordValidation(e) {
      let passRegex = new RegExp("^[a-zA-Z0-9]{6}$");
			let passIsValid = passRegex.test(e.target.value);
			passIsValid? this.isPasswordInvalid = false: this.isPasswordInvalid = true; this.isDisableBtn = true
			this.checkingBtnIsDisabled();
		},
		checkingBtnIsDisabled (){
			if(
				this.isNameInvalid  &&
				this.isPhoneNumberInvalid &&
				this.isPasswordInvalid 
	  	) {
				this.isDisableBtn = true
			} else if(
				!this.isNameInvalid && this.name.length > 0 &&
				!this.isPhoneNumberInvalid && this.phoneNumber.length > 0 &&
				!this.isPasswordInvalid && this.password.length >= 5
	  	) {
				this.isDisableBtn = false;
			}
		}
	},
};
</script>
<style scoped>
	.disableBtn {
		background: #757575;
		color: #ffffff
	}
	.ableBtn {
		background: #000000;
		color: #ffffff
	}
	.mt-3 {
		margin-top: 3rem;
	}
	.group {
		position: relative;
	}
	.submit-btn {
		background: #a1a1a1;
		color: #ffffff;
	}
	input {
		font-size: 18px;
		padding: 10px 10px 10px 5px;
		display: block;
		border: none;
		border: 2px solid #e2e2e2;
		border-radius: 5px;
		width: 100%;
	}
	input:focus {
		outline: none;
	}

	label {
		color: #757575;
		font-size: 18px;
		font-weight: normal;
		position: absolute;
		pointer-events: none;
		top: 8px;
		transition: 0.2s ease all;
		-moz-transition: 0.2s ease all;
		-webkit-transition: 0.2s ease all;
		margin-right: 10px;
		background: #ffffff;
		width: auto;
		padding-right: 8px;
		padding-left: 8px;
	}

	input:focus ~ label,
	input:valid ~ label {
		top: -10px;
		font-size: 14px;
	}
	input:focus ~ input:focus {
		width: 50%;
	}
	.font-size-12 {
		font-size: 12px;
	}

	.redBorder {
		border: 2px solid red;
	}

	.redColor {
		color: red;
	}

	:-webkit-autofill {
		animation-name: onAutoFillStart;
	}
	:not(:-webkit-autofill) {
		animation-name: onAutoFillCancel;
	}

	.bold {
		font-weight: bold;
	}

	.text-center {
		text-align: center;
	}

	.mt-1 {
		margin-top: 1rem;
	}
	.enaleBtn {
		background-color: seagreen;
	}
</style>