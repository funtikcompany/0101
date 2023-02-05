<template>
  <div class="container">
    <div class="user">
      <div class="user-wrapper">
        <div class="user-about">
          <img src="@/img/user-icon.png" class="user-photo" alt="user">
          <div class="user-info">
            <h3 class="user-name">
              Eva Jonson
            </h3>
            <span class="user-prof">Sales Manager</span>
            <p class="user-description">I will find the best offers for you. <br> My services are absolutely free.</p>
          </div>
        </div>
        <div class="services">
          <p class="services-title">Services</p>
          <div class="services-table">
            <div class="services-item">
              <div class="services-box">
                <progress class="progress progress-green" value="11" max="15"></progress>
                <span class="services-name">Manual tour booking</span>
              </div>
              <span class="services-number">11</span>
            </div>
            <div class="services-item">
              <div class="services-box">
                <progress class="progress progress-blue" value="3" max="15"></progress>
                <span class="services-name">Package tours</span>
              </div>
              <span class="services-number">3</span>
            </div>
            <div class="services-item">
              <div class="services-box">
                <progress class="progress progress-blue" value="1" max="13"></progress>
                <span class="services-name">Hotels</span>
              </div>
              <span class="services-number">1</span>
            </div>
          </div>
          <div class="services-total"><span>Total</span><span class="services-number">15</span></div>
        </div>
        <div class="reviews">
          <div class="reviews-nav">
            <div class="reviews-nav-left">
              <h4 class="reviews-title">
                Latest reviews
              </h4>
              <a class="reviews-all" href="">All reviews</a>
            </div>
            <div class="reviews-nav-right">
              <span class="reviews-icon likes-icon">
                131
              </span>
              <span class="reviews-icon comments-icon">
                14
              </span>
            </div>
          </div>
        </div>
        <div v-if="userComments.length != 0" class="comments">
          <Comments v-for="(comment, index) in userComments" :comment="comment" :key="index">
          </Comments>
        </div>
        <div v-else class="comments">
          <p class="no-comments">There are no comments yet. You can be the first!</p>
        </div>
      </div>
      <div class="area">
        <textarea @keyup.enter="showUserComment()" v-model="inputValue" class="area-input" type="text">
        </textarea>
        <div @click="showUserComment()" class="btn">Send a message</div>
      </div>

    </div>
    <div v-if="show" class="popup">
      <p class="popup-title">Create a login</p>
      <input @keyup.enter="hidePopup()" v-model="userName" class="popup-input" type="text">
      <div @click="hidePopup()" class="btn">Ok</div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Comment from "@/components/Comment.vue";
export default {
  name: 'UserPage',
  components: {
    Comments: Comment
  },
  data() {
    return {
      inputValue: '',
      userName: '',
      show: false,
      userComments: [
        {
          title: 'Samuel Jackson',
          decscription: "Hey Eva! You're cool.Nice pic!",
          date: 'Apr 13 2022'
        },
        {
          title: 'Angela Deimon',
          decscription: "Thanks for your services! We really liked the ocean view room. We hope to cooperate in the near future.We are sure you will do everything to make our next holiday fantastic.",
          date: 'Apr 10 2022'
        },
        {
          title: 'Ronald Harris',
          decscription: "Eva, hello! There is such a question: How can I contact you if I am abroad in roaming?",
          date: 'Apr 8 2022'
        }
      ],
    }
  }, methods: {
    showUserComment() {
      if (this.inputValue != '') {
        console.log(this.userName)
        let options = {
          year: 'numeric',
          month: 'short',
          day: 'numeric',
          timezone: 'UTC'
        };

        let date = new Date().toLocaleString("en", options)
        this.userComments.push({
          title: this.userName,
          decscription: this.inputValue,
          date: date
        })
        localStorage.setItem('comments', JSON.stringify(this.userComments));
        this.inputValue = ''
      } else {
        alert("Enter comment")
      }
    },
    createComment() {
      this.userComments = JSON.parse(localStorage.getItem('comments'))
    },
    hidePopup() {
      if (this.userName != '') {
        localStorage.setItem('userName', JSON.stringify(this.userName));
        console.log(this.userName)
        this.show = false
      } else {
        alert("Enter Login")
      }

    }
  },
  mounted() {
    if (localStorage.getItem('userName')) {
      this.userName = JSON.parse(localStorage.getItem('userName'))
      this.show = false
    } else {
      this.show = true
    }

    if (localStorage.getItem('comments')) {
      this.createComment()
    }

  }
}
</script>
