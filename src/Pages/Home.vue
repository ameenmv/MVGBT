<template>
  <div class="p-8 py-4 h-[100vh] rounded-[40px] border-t border-b">
    <div class="flex">
      <!-- left -->
      <div class="w-[20%] pr-8">
        <div class="logo gap-1 flex items-center">
          <img class="w-[60px]" src="../assets/logo.png" alt="" />
          <p class="fruktur-regular text-[20px]">MVGBT</p>
        </div>
        <div class="pl-4 mt-6 pr-4">
          <div class="btn">
            <div class="font-bold">+</div>
            &nbsp; New Chat
            <img class="w-[25px] ml-2" src="../assets/star.png" alt="" />
          </div>
        </div>
        <div class="mt-10 bg-[black] opacity-[.3] h-[1px] w-[100%]"></div>
        <p class="opacity-[.6] mt-6">Today</p>
        <p v-for="text in texts" :key="text.id" class="mt-3">
          {{ text.slice(0, 30) + (text.length > 30 ? "..." : "") }}
        </p>
        <p class="opacity-[.6] mt-6">Yesterday</p>
        <p v-for="text in texts" :key="text.id" class="mt-3">
          {{ text.slice(0, 30) + (text.length > 30 ? "..." : "") }}
        </p>
      </div>
      <!-- right -->
      <div class="w-[80%] border-l h-[98vh] p-3 pt-9">
        <!-- header -->
        <div class="flex items-center justify-between">
          <div class="flex items-center justify-center gap-4">
            <p class="fruktur-regular text-[20px]">MVGBT</p>
            <p
              class="p-1 py-[1px] text-[14px] border border-[var(--border)] bg-[var(--sc)] rounded-[5px]"
            >
              plus
            </p>
          </div>
          <div class="flex gap-2">
            <div
              class="btn flex gap-2 !bg-[white] border border-[var(--border)] !text-[black] !py-[8px]"
            >
              Share
              <svg
                width="20px"
                fill="black"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 640 640"
              >
                <path
                  d="M342.6 73.4C330.1 60.9 309.8 60.9 297.3 73.4L169.3 201.4C156.8 213.9 156.8 234.2 169.3 246.7C181.8 259.2 202.1 259.2 214.6 246.7L288 173.3L288 384C288 401.7 302.3 416 320 416C337.7 416 352 401.7 352 384L352 173.3L425.4 246.7C437.9 259.2 458.2 259.2 470.7 246.7C483.2 234.2 483.2 213.9 470.7 201.4L342.7 73.4zM160 416C160 398.3 145.7 384 128 384C110.3 384 96 398.3 96 416L96 480C96 533 139 576 192 576L448 576C501 576 544 533 544 480L544 416C544 398.3 529.7 384 512 384C494.3 384 480 398.3 480 416L480 480C480 497.7 465.7 512 448 512L192 512C174.3 512 160 497.7 160 480L160 416z"
                />
              </svg>
            </div>
            <div class="btn !py-[8px]">
              New Chat
              <img class="w-[25px] ml-2" src="../assets/star.png" alt="" />
            </div>
          </div>
        </div>
        <!-- chat -->
        <div
          class="my-6 flex flex-col justify-center items-center mx-10 rounded-[10px] w-[100%] h-[82vh] bg-[var(--sc)]"
        >
          <!-- chat area -->
          <div
            v-if="chat.length"
            class="flex-1 overflow-y-auto my-6 mx-10 rounded-[10px] w-[100%] bg-[var(--sc)] p-4"
          >
            <div v-for="(msg, i) in chat" :key="i" class="mb-3">
              <div
                :class="[
                  'inline-block px-3 py-2 rounded-lg',
                  msg.role === 'user'
                    ? 'bg-blue-500 text-white self-end'
                    : 'bg-gray-200 text-black self-start',
                ]"
              >
                {{ msg.text }}
              </div>
            </div>
          </div>
          <!-- input -->
          <div class="flex justify-center w-[65%] input">
            <div
              class="bg-[white] border w-[100%] border-[var(--border)] rounded-[40px] outline-none p-4 flex flex-col"
              type="text"
            >
              <div class="flex gap-1">
                <svg
                  width="15px"
                  fill="black"
                  class="opacity-[.6]"
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 640 640"
                >
                  <path
                    d="M295.4 37L310.2 73.8L347 88.6C350 89.8 352 92.8 352 96C352 99.2 350 102.2 347 103.4L310.2 118.2L295.4 155C294.2 158 291.2 160 288 160C284.8 160 281.8 158 280.6 155L265.8 118.2L229 103.4C226 102.2 224 99.2 224 96C224 92.8 226 89.8 229 88.6L265.8 73.8L280.6 37C281.8 34 284.8 32 288 32C291.2 32 294.2 34 295.4 37zM142.7 105.7L164.2 155.8L214.3 177.3C220.2 179.8 224 185.6 224 192C224 198.4 220.2 204.2 214.3 206.7L164.2 228.2L142.7 278.3C140.2 284.2 134.4 288 128 288C121.6 288 115.8 284.2 113.3 278.3L91.8 228.2L41.7 206.7C35.8 204.2 32 198.4 32 192C32 185.6 35.8 179.8 41.7 177.3L91.8 155.8L113.3 105.7C115.8 99.8 121.6 96 128 96C134.4 96 140.2 99.8 142.7 105.7zM496 368C502.4 368 508.2 371.8 510.7 377.7L532.2 427.8L582.3 449.3C588.2 451.8 592 457.6 592 464C592 470.4 588.2 476.2 582.3 478.7L532.2 500.2L510.7 550.3C508.2 556.2 502.4 560 496 560C489.6 560 483.8 556.2 481.3 550.3L459.8 500.2L409.7 478.7C403.8 476.2 400 470.4 400 464C400 457.6 403.8 451.8 409.7 449.3L459.8 427.8L481.3 377.7C483.8 371.8 489.6 368 496 368zM492 64C503 64 513.6 68.4 521.5 76.2L563.8 118.5C571.6 126.4 576 137 576 148C576 159 571.6 169.6 563.8 177.5L475.6 265.7L374.3 164.4L462.5 76.2C470.4 68.4 481 64 492 64zM76.2 462.5L340.4 198.3L441.7 299.6L177.5 563.8C169.6 571.6 159 576 148 576C137 576 126.4 571.6 118.5 563.8L76.2 521.5C68.4 513.6 64 503 64 492C64 481 68.4 470.4 76.2 462.5z"
                  />
                </svg>
                <input
                  @keyup.enter="sendMessage"
                  v-model="input"
                  class="p-2 outline-none w-[100%]"
                  type="text"
                  placeholder="Ask me anything..."
                />
              </div>
              <div class="flex mt-3 justify-between items-center">
                <div
                  class="btn border border-[var(--border)] !text-[black] flex !bg-[white] !py-[8px]"
                >
                  Select Source &nbsp;
                  <div class="rotate-[180deg]">^</div>
                </div>
                <div class="flex gap-2">
                  <div
                    class="btn flex gap-2 !bg-[white] border border-[var(--border)] !text-[black] !px-[10px] !py-[5px]"
                  >
                    <svg
                      width="20px"
                      fill="black"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 640 640"
                    >
                      <path
                        d="M451.5 160C434.9 160 418.8 164.5 404.7 172.7C388.9 156.7 370.5 143.3 350.2 133.2C378.4 109.2 414.3 96 451.5 96C537.9 96 608 166 608 252.5C608 294 591.5 333.8 562.2 363.1L491.1 434.2C461.8 463.5 422 480 380.5 480C294.1 480 224 410 224 323.5C224 322 224 320.5 224.1 319C224.6 301.3 239.3 287.4 257 287.9C274.7 288.4 288.6 303.1 288.1 320.8C288.1 321.7 288.1 322.6 288.1 323.4C288.1 374.5 329.5 415.9 380.6 415.9C405.1 415.9 428.6 406.2 446 388.8L517.1 317.7C534.4 300.4 544.2 276.8 544.2 252.3C544.2 201.2 502.8 159.8 451.7 159.8zM307.2 237.3C305.3 236.5 303.4 235.4 301.7 234.2C289.1 227.7 274.7 224 259.6 224C235.1 224 211.6 233.7 194.2 251.1L123.1 322.2C105.8 339.5 96 363.1 96 387.6C96 438.7 137.4 480.1 188.5 480.1C205 480.1 221.1 475.7 235.2 467.5C251 483.5 269.4 496.9 289.8 507C261.6 530.9 225.8 544.2 188.5 544.2C102.1 544.2 32 474.2 32 387.7C32 346.2 48.5 306.4 77.8 277.1L148.9 206C178.2 176.7 218 160.2 259.5 160.2C346.1 160.2 416 230.8 416 317.1C416 318.4 416 319.7 416 321C415.6 338.7 400.9 352.6 383.2 352.2C365.5 351.8 351.6 337.1 352 319.4C352 318.6 352 317.9 352 317.1C352 283.4 334 253.8 307.2 237.5z"
                      />
                    </svg>
                    Attach
                  </div>
                  <div
                    class="btn flex gap-2 !bg-[white] border border-[var(--border)] !text-[black] !px-[10px] !py-[5px]"
                  >
                    <svg
                      width="20px"
                      fill="black"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 640 640"
                    >
                      <path
                        d="M320 64C267 64 224 107 224 160L224 288C224 341 267 384 320 384C373 384 416 341 416 288L416 160C416 107 373 64 320 64zM176 248C176 234.7 165.3 224 152 224C138.7 224 128 234.7 128 248L128 288C128 385.9 201.3 466.7 296 478.5L296 528L248 528C234.7 528 224 538.7 224 552C224 565.3 234.7 576 248 576L392 576C405.3 576 416 565.3 416 552C416 538.7 405.3 528 392 528L344 528L344 478.5C438.7 466.7 512 385.9 512 288L512 248C512 234.7 501.3 224 488 224C474.7 224 464 234.7 464 248L464 288C464 367.5 399.5 432 320 432C240.5 432 176 367.5 176 288L176 248z"
                      />
                    </svg>
                    Voice
                  </div>
                  <div
                    @click="sendMessage"
                    class="btn flex gap-2 border border-[var(--border)] !px-[10px] !py-[5px]"
                  >
                    <svg
                      width="20px"
                      fill="white"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 640 640"
                    >
                      <path
                        d="M342.6 81.4C330.1 68.9 309.8 68.9 297.3 81.4L137.3 241.4C124.8 253.9 124.8 274.2 137.3 286.7C149.8 299.2 170.1 299.2 182.6 286.7L288 181.3L288 552C288 569.7 302.3 584 320 584C337.7 584 352 569.7 352 552L352 181.3L457.4 286.7C469.9 299.2 490.2 299.2 502.7 286.7C515.2 274.2 515.2 253.9 502.7 241.4L342.7 81.4z"
                      />
                    </svg>
                    Send
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="mt-6 flex text-[15px]">
            <div class="opacity-[.6]">
              Centra may display inaccurate info, so please double check the
              response. &nbsp;
            </div>
            <div class="!opacity-[1] underline">Your Privacy & MVGPT</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      input: "",
      chat: [],
      texts: [
        `ChatGPT is a language model developed by OpenAI, based on the GPT-3.5 architecture. It is designed to understand and generate human-like text based on the input it receives. ChatGPT can perform a variety of tasks, including answering questions, providing explanations, generating creative content, and engaging in conversations on a wide range of topics.`,
        `It has been trained on a diverse dataset that includes books, articles, websites, and other text sources, allowing it to have a broad understanding of language and knowledge up to its training cutoff date in September 2021. Users can interact with ChatGPT through text-based interfaces, making it a versatile tool for various applications such as customer support, content creation, tutoring, and more.`,
      ],
    };
  },
  methods: {
    sendMessage() {
      if (!this.input.trim()) return;

      // أضيف رسالة المستخدم
      this.chat.push({ role: "user", text: this.input });

      // رد تجريبي من البوت
      setTimeout(() => {
        this.chat.push({ role: "bot", text: "رد تلقائي على: " + this.input });
      }, 800);

      // امسح الانبوت
      this.input = "";
    },
  },
};
</script>

<style lang="scss" scoped>
.input {
  transition: 0.5s;
}
</style>
