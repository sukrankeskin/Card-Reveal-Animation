<template>
  <div class="wrapp">
    <section class="section">
      <h1 class="title">
        Cards Reveal <br />
        Animation
      </h1>
      <div class="card__tabs">
        <div class="card__tabs-body">
          <div class="tab__b1-bg">
            <div v-for="n in 10" :key="n" class="tab__b1-bg-ln"></div>
          </div>
          <div class="card__tabs-body-wr">
            <div
              v-for="(tab, index) in tabs"
              :key="index"
              :class="['tab__b1', { active: activeTabIndex === index }]"
            >
              <div class="tab__b1-wrapp">
                <div class="tab__b1-title">{{ tab.title }}</div>
                <p v-if="tab.content" class="tab__b1-p">{{ tab.content }}</p>
                <div v-if="tab.details" class="tab__b1-title">
                  Here is how I can do it
                </div>
                <ul v-if="tab.details" class="tab__b1-ul">
                  <li
                    v-for="(detail, detailIndex) in tab.details"
                    :key="detailIndex"
                    class="tab__b1-li"
                  >
                    {{ detail }}
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>
        <div class="card__tabs-header">
          <ul class="tab">
            <li
              v-for="(tab, index) in tabs"
              :key="index"
              :class="['tab__item', { active: activeTabIndex === index }]"
              @click="changeTab(index)"
            >
              {{ tab.tabName }}
            </li>
          </ul>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import { ref } from "vue";
import { gsap } from "gsap";

export default {
  name: "CardRevealAnimation",
  setup() {
    const activeTabIndex = ref(0);

    const tabs = [
      {
        tabName: "Consultation",
        title: "1 Consultation",
        content:
          "Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas hic pariatur deserunt maxime rerum accusantium nesciunt aut praesentium consequatur sapiente. Lorem ipsum dolor sit amet consectetur, adipisicing elit. Voluptatem, qui? Lorem ipsum dolor sit amet consectetur, adipisicing elit. Culpa, deserunt.",
      },
      {
        tabName: "UX Strategy",
        title: "2 UX Strategy",
        content: "",
        details: [
          "Discovery phases",
          "ux roadmap",
          "Stakeholder engagement",
          "Competitor analysis",
        ],
      },
      {
        tabName: "User Research",
        title: "3 User Research",
        content:
          "Lorem ipsum dolor sit amet consectetur adipisicing elit. Vel hic dolor officia, esse animi corrupti iusto omnis! Quo, molestias modi?",
        details: [
          "Discovery phases",
          "ux roadmap",
          "Stakeholder engagement",
          "Competitor analysis",
        ],
      },
      {
        tabName: "UI Design",
        title: "4 UI Design",
        content:
          "Lorem ipsum dolor sit amet consectetur adipisicing elit. Harum porro quo quidem ducimus provident, eum quod. Minus voluptatibus eos necessitatibus?",
        details: [
          "Discovery phases",
          "ux roadmap",
          "Stakeholder engagement",
          "Competitor analysis",
        ],
      },
      {
        tabName: "Development",
        title: "5 Development",
        content:
          "Lorem ipsum dolor, sit amet consectetur adipisicing elit. Omnis harum delectus iste recusandae architecto facere accusamus, sit odit quaerat reprehenderit?",
        details: [
          "Discovery phases",
          "ux roadmap",
          "Stakeholder engagement",
          "Competitor analysis",
        ],
      },
    ];

    const changeTab = (index) => {
      const t1 = gsap.timeline();
      t1.to(".tab__b1-bg .tab__b1-bg-ln", 0.3, {
        background: "#a0671275",
        stagger: {
          amount: 0.3,
          from: "start",
        },
        ease: "none",
      }).to(
        ".tab__b1-bg .tab__b1-bg-ln",
        0.3,
        {
          background: "#18181875",
          stagger: {
            amount: 0.3,
            from: "start",
          },
          ease: "none",
        },
        "-=.2"
      );

      const currentTabB1Txt = document
        .querySelectorAll(".tab__b1")
        [index].querySelector(".tab__b1-wrapp");

      const t1Txt = gsap.timeline();
      t1Txt
        .to(".tab__b1.active .tab__b1-wrapp", 0.3, {
          clipPath: "polygon(0% 100%, 100% 100%, 100% 100%, 0% 100%)",
          opacity: 0,
          ease: "none",
          onComplete: () => {
            activeTabIndex.value = index;
          },
        })
        .fromTo(
          currentTabB1Txt,
          {
            clipPath: "polygon(0% 0%, 100% 0%, 100% 0%, 0% 0%)",
            opacity: 0,
          },
          {
            delay: 0.2,
            clipPath: "polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)",
            opacity: 1,
            ease: "none",
          }
        );
    };

    return {
      tabs,
      activeTabIndex,
      changeTab,
    };
  },
};
</script>

<style>
@import url("../assets/styles/styles.css");

/* Add any additional styles if needed */
</style>
