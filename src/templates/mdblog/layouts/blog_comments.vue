<template>
    <div id="blog-comments" class="mdui-shadow-2 mdui-hoverable" style="padding: 40px;margin-top: 15px;">
          <div class="mdui-valign" style="margin-bottom: 30px;" v-if="uid">
              <div class="mdui-textfield mdui-textfield-floating-label mdui-float-left" style="width: 95%;margin-right: 20px;">
                  <label class="mdui-textfield-label">评论</label>
                  <textarea v-model="commentContent" class="mdui-textfield-input mdui-float-left-right" ></textarea>

              </div>
              <button class ="mdblog-comment-send-btn mdui-btn mdui-btn-icon" :class="{ disabled: commentPosting }"
              @click="postComment"><i class="mdui-icon material-icons">send</i></button>
          </div>
          <div class="mdblog-comments mdui-container">
              <div class="mdblog-comment mdui-row" style="margin-top: 50px;padding-right: 30px;" v-for="comment in comments">
                  <div class="mdui-col-xs-1">
                      <img class="mdui-img-circle mdui-img-fluid" :src="BlogGlobals.picAddress + '/upload/usericon/' + comment.Author.UID + '.png'"
                           :href="BlogGlobals.luoguAddress +'/space/show?uid=' + comment.Author.UID"
                           target="_blank">
                  </div>
                  <div class="mdui-col-xs-11">
                      <div class="mdui-typo-body-1-opacity mdui-typo">{{ comment.Content }}&nbsp;</div>
                      <div class="mdui-typo"><hr/></div>
                      <a class="mdui-float-left mdui-typo-caption-opacity mdblog-comment-username" :href="BlogGlobals.luoguAddress +'/space/show?uid=' + comment.Author.UID">By {{ comment.Author.Username }}</a>
                      <div class="mdui-typo-caption-opacity mdui-float-right">At {{ comment.ReplyTime | formatDate }}</div>
                  </div>
              </div>
              <div class="mdui-valign" style="margin: 30px;" v-if="ready">
                  <div class="mdui-center">
                      <div class="mdui-btn-group" v-if="totalPages > 1">
                          <a @click="getComments(1)" :class="{ disabled: page == 1 }" class="mdui-btn"><i class="mdui-icon material-icons">first_page</i></a>
                          <a @click="getComments(page - 1)" :class="{ disabled: page == 1 }" class="mdui-btn"><i class="mdui-icon material-icons">keyboard_arrow_left</i></a>
                          <a @click="getComments(page - 2)" v-if="page - 2 >= 1" class="mdui-btn">{{ page - 2 }}</a>
                          <a @click="getComments(page - 1)" v-if="page - 1 >= 1" class="mdui-btn">{{ page - 1 }}</a>
                          <a class="mdui-btn-active mdui-btn">{{ page }}</a>
                          <a @click="getComments(page + 1)" v-if="page + 1 <= totalPages" class="mdui-btn">{{ page + 1 }}</a>
                          <a @click="getComments(page + 2)" v-if="page + 2 <= totalPages" class="mdui-btn">{{ page + 2 }}</a>
                          <a @click="getComments(page + 1)" :class="{ disabled: page == totalPages }" class="mdui-btn"><i class="mdui-icon material-icons">keyboard_arrow_right</i></a>
                          <a @click="getComments(totalPages)" :class="{ disabled: page == totalPages }"  class="mdui-btn"><i class="mdui-icon material-icons">last_page</i></a>
                      </div>
                  </div>
              </div>
          </div>
      </div>
</template>

<script>
  import { defaultData, defaultMounted, getComments, postComment } from 'scripts/article_comments'
  import formatDate from 'plugins/format_date'
  export default {
    data: defaultData,
    mounted: defaultMounted,
    methods: { getComments, postComment },
    filters: { formatDate }
  }
</script>
