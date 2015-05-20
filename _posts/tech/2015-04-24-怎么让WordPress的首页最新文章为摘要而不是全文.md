---
layout: post
title: 怎么让WordPress的首页最新文章为摘要而不是全文
description: 解决使用wordpress的主题时首页全文显示的问题
category: tech
---

######2015-04-24-怎么让WordPress的首页最新文章为摘要而不是全文.md


* * *

> 提示：本文针对WordPress的Twenty Twelve主题进行的修改，其他主题都类似修改

* * *

由于文章太长，将全文摆放在首页难看且浪费网络资源，百度之后，发现有以下解决方案。

  1. WordPress准许用户在`外观->编辑`中修改本WordPress使用的主题。
  2. 打开`控制台->外观->编辑->index.php`可以看到以下代码

        <?php /* Start the Loop */ ?>
        <?php while ( have_posts() ) : the_post(); ?>
            <?php get_template_part( 'content', get_post_format() ); ?>
        <?php endwhile; ?>

        
    这段代码的意思是在首页index.php页面将文章呈现出来，使用content.php 模板显示这些内容。因此打开`content.php`的编辑页面，找到下面的代码
        
        <div class="entry-content">
            <?php the_content( __( 'Continue reading <span class="meta-nav">&rarr;</span>', 'twentytwelve' ) ); ?>
            <?php wp_link_pages( array( 'before' => '<div class="page-links">' . __( 'Pages:', 'twentytwelve' ), 'after' => '</div>' ) ); ?>
        </div><!-- .entry-content -->

    
    将Continue reading这一段给注释掉，替代成下面的代码
    
        <?php if(!is_single()) {
            the_excerpt();
        } else {
            the_content(__('(more…)'));
        } ?>   
    
    保存之后，打开首页就可以看到摘要了。
    

  3. 修改以上内容后会发现文章题目下会有一个没有评论的链接。这个是没有任何意义的，依然找到`content.php`，注释掉`<div class="comments-link">`所在的if段落，即下面这段代码注释掉。 

        <?php if ( comments_open() ) : ?>
            <div class="comments-link">
                <?php comments_popup_link( '<span class="leave-reply">' . __( 'Leave a reply', 'twentytwelve' ) . '</span>', __( '1 Reply', 'twentytwelve' ), __( '% Replies', 'twentytwelve' ) ); ?>
            </div>
            <!-- .comments-link -->
        <?php endif; // comments_open() ?>
