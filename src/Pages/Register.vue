<template>
  <div
    class="h-[100vh] w-[100vw] flex justify-center items-center bg-[var(--bg)]"
  >
    <div class="flex w-[100%]">
      <div class="w-[50%] flex justify-center items-center">
        <div class="w-[50%]">
          <p class="text-[35px] font-bold">Sign Up</p>
          <p class="mt-1 font-medium">Free forever. No Credit Card Needed.</p>
          <div class="input cursor-pointer mt-6">
            <svg
              width="25px"
              class="mr-2"
              fill="black"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 640 640"
            >
              <path
                d="M564 325.8C564 467.3 467.1 568 324 568C186.8 568 76 457.2 76 320C76 182.8 186.8 72 324 72C390.8 72 447 96.5 490.3 136.9L422.8 201.8C334.5 116.6 170.3 180.6 170.3 320C170.3 406.5 239.4 476.6 324 476.6C422.2 476.6 459 406.2 464.8 369.7L324 369.7L324 284.4L560.1 284.4C562.4 297.1 564 309.3 564 325.8z"
              />
            </svg>
            Sign Up With Google
          </div>
          <div class="input cursor-pointer mt-5">
            <svg
              width="30px"
              class="mr-2"
              fill="black"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 640 640"
            >
              <path
                d="M447.1 332.7C446.9 296 463.5 268.3 497.1 247.9C478.3 221 449.9 206.2 412.4 203.3C376.9 200.5 338.1 224 323.9 224C308.9 224 274.5 204.3 247.5 204.3C191.7 205.2 132.4 248.8 132.4 337.5C132.4 363.7 137.2 390.8 146.8 418.7C159.6 455.4 205.8 545.4 254 543.9C279.2 543.3 297 526 329.8 526C361.6 526 378.1 543.9 406.2 543.9C454.8 543.2 496.6 461.4 508.8 424.6C443.6 393.9 447.1 334.6 447.1 332.7zM390.5 168.5C417.8 136.1 415.3 106.6 414.5 96C390.4 97.4 362.5 112.4 346.6 130.9C329.1 150.7 318.8 175.2 321 202.8C347.1 204.8 370.9 191.4 390.5 168.5z"
              />
            </svg>
            Sign Up With Apple
          </div>
          <div
            class="relative flex my-8 justify-center items-center opacity-[.3]"
          >
            <p class="px-3 bg-[white]">OR</p>
            <div class="line"></div>
          </div>
          <!-- name -->
          <label for="">Your Name</label>
          <input
            v-model="form.name"
            @input="setTouched('name')"
            :class="v$.form.name.$error ? 'is-invalid' : ''"
            placeholder="Your Name"
            type="text"
            class="input mt-2"
          />
          <div v-if="v$.form.name.$errors.length">
            <div
              v-for="error in v$.form.name.$errors"
              :key="error.$uid"
              class="text-red-500 mt-1 font-medium"
            >
              {{ error.$message }}
            </div>
          </div>
          <!-- email -->
          <div class="mt-6">
            <label for="">Your Email</label>
            <input
              v-model="form.email"
              @input="setTouched('email')"
              placeholder="Your Email"
              :class="v$.form.email.$error ? 'is-invalid' : ''"
              type="email"
              class="input mt-2"
            />
            <div v-if="v$.form.email.$errors.length">
              <div
                v-for="error in v$.form.email.$errors"
                :key="error.$uid"
                class="text-red-500 mt-1 font-medium"
              >
                {{ error.$message }}
              </div>
            </div>
          </div>
          <!-- password -->
          <div class="mt-6">
            <label for="">Your Password</label>
            <input
              v-model="form.password"
              @input="setTouched('password')"
              :class="v$.form.password.$error ? 'is-invalid' : ''"
              placeholder="Your Password"
              type="password"
              class="input mt-2"
            />
            <div v-if="v$.form.password.$errors.length">
              <div
                v-for="error in v$.form.password.$errors"
                :key="error.$uid"
                class="text-red-500 mt-1 font-medium"
              >
                {{ error.$message }}
              </div>
            </div>
          </div>
          <div class="flex mt-6 gap-3 font-medium items-center">
            <input class="w-[16px] h-[16px]" type="checkbox" />
            <p>
              I agree to all th Term,
              <span class="text-[var(--purple)]">Privacy Policy</span> and
              <span class="text-[var(--purple)]">fees.</span>
            </p>
          </div>
          <!-- submit -->
          <div
            @click="submit"
            type="submit"
            value="Submit"
            class="input mt-6 !bg-[var(--purple)] text-[white] cursor-pointer"
          >
            Submit
          </div>
          <div class="mt-6 font-medium">
            Have an account?
            <router-link to="/login"
              ><span class="text-[var(--purple)]">Login</span></router-link
            >
          </div>
        </div>
      </div>
      <div class="w-[50%]">
        <img
          class="border border-[var(--border)] rounded-[20px] w-[70%]"
          src="../assets/signup.png"
          alt=""
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive } from "vue";
import useVuelidate from "@vuelidate/core";
import { required, email, minLength } from "@vuelidate/validators";
import { useToast } from "vue-toastification";
import axios from "axios";
import { useRouter } from "vue-router";
const toast = useToast();
const router = useRouter();

const form = reactive({
  name: "",
  email: "",
  password: "",
});

const rules = {
  form: {
    name: { required, minLength: minLength(3) },
    email: { required, email },
    password: { required, minLength: minLength(4) },
  },
};

const v$ = useVuelidate(rules, { form });

const setTouched = (field) => {
  if (field === "name" || field === "all") v$.value.form.name.$touch();
  if (field === "email" || field === "all") v$.value.form.email.$touch();
  if (field === "password" || field === "all") v$.value.form.password.$touch();
};

// submit
const submit = async () => {
  setTouched("all");
  const valid = await v$.value.$validate();

  if (!valid) {
    toast.error("من فضلك املأ البيانات بشكل صحيح");
    return;
  }

  try {
    // form data
    const formData = {
      name: form.name,
      email: form.email,
      password: form.password,
      provider: "mgr",
    };

    // send to api
    const response = await axios.post(
      "http://127.0.0.1:8000/api/users",
      formData
    );

    console.log("📥 Response:", response.data);
    if (response.data.status === 200) {
      toast.success("✅ تسجيل الدخول ناجح");
      setTimeout(() => {
        router.push("/");
      }, 1000);
    } else {
      toast.error(response.data.message || "بيانات غير صحيحة");
    }
  } catch (error) {
    console.error("❌ Error:", error.response?.data || error.message);
    // delete this before deadline
    toast.error(error.response?.data?.message || "حدث خطأ أثناء تسجيل الدخول");
  }
};
</script>

<style lang="scss" scoped>
.input {
  padding: 14px 20px;
  border-radius: 10px;
  border: 1px solid var(--border);
  background-color: var(--sc);
  width: 100%;
  outline: none;
  font-weight: 500;
  display: flex;
  justify-content: center;
  align-items: center;
}
.line {
  position: absolute;
  width: 100%;
  height: 1px;
  background-color: var(--black);
  z-index: -1;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
label {
  font-weight: 500;

  font-size: 18px;
}
</style>
