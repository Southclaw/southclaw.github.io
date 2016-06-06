---
layout:     post
title:      "Category Pages on WordPress"
date:       2014-11-12 16:19:42
categories: web
---
Here's a quick post outlining some small changes I've made to the PHP code on my university WordPress 4.0 site which students use to document course work. I originally wanted a very organised site where I could store posts of different types (course strands in most contexts) in separate pages and still leave the main page as a full feed of all my content. Pages, unfortunately didn't offer this behaviour by default as they only displayed a pre-set (static) piece of content.  I decided to delve into a language I've rarely touched on on a platform I've never even read the API documentation for! After a couple of hours of work and Wordpress codex browsing, I have exactly what I want. 
<!--more-->

{% highlight php %}
<?php
/**
 * The template for displaying all pages.
 *
 * This is the template that displays all pages by default.
 * Please note that this is the WordPress construct of pages
 * and that other 'pages' on your WordPress site will use a
 * different template.
 *
 * @package SemPress
 * @since SemPress 1.0.0
 */

get_header(); ?>

	<section id="primary">
	<main id="content" role="main">

	<div id="content" class="narrowcolumn" role="main">
	
	<?php if (have_posts()) : while (have_posts()) : the_post(); ?>
	<div class="post" id="post-<?php the_ID(); ?>">
	<h2><?php the_title(); ?></h2>
		<div class="entry">
			<?php the_content('<p class="serif">Read the rest of this page &raquo;</p>'); ?>
	
			<?php wp_link_pages(array('before' => '<p><strong>Pages:</strong> ', 'after' => '</p>', 'next_or_number' => 'number')); ?>
	
		</div>
	</div>
	<?php endwhile; endif; ?>
	<?php
	$catname = get_the_title();

	if($catname != "About")
	{
		$catid = get_cat_ID($catname);

		if($catid > 0)
		{
			$catq = "cat=$catid";
			$the_query = new WP_Query($catq);

			if ( $the_query->have_posts() )
			{
				while($the_query->have_posts())
				{
					$the_query->the_post();

					?>

					<article <?php sempress_post_id(); ?> <?php post_class(); ?><?php sempress_semantics("post"); ?>>
					<header class="entry-header">
					<h1 class="entry-title p-name" itemprop="name headline"><a href="<?php the_permalink(); ?>" class="u-url url" title="<?php printf( esc_attr__( 'Permalink to %s', 'sempress' ), the_title_attribute( 'echo=0' ) ); ?>" rel="bookmark" itemprop="url"><?php the_title(); ?></a></h1>

					<?php if ( get_post_type() == 'post' ) : ?>
						<div class="entry-meta">
						<?php sempress_posted_on(); ?>
						</div><!-- .entry-meta -->
					<?php endif; ?>
					</header><!-- .entry-header -->

					<div class="entry-summary p-summary" itemprop="description">
					<?php the_excerpt(); ?>
					</div><!-- .entry-summary -->

					<?php get_template_part( 'entry', 'footer' ); ?>
					</article><!-- #post-<?php the_ID(); ?> -->

					<?php

					echo "<br />";
				}
			}
			wp_reset_postdata();
		}
	}
	?>
	<?php comments_template(); ?>

	</main><!-- #content -->
	</section><!-- #primary -->

<?php get_sidebar(); ?>
<?php get_footer(); ?>
{% endhighlight %}

The idea here is that, if a page is named after a category then it will display all the posts in that category (as well as whatever content the page body text contains). Firstly, the page name is stored into "$catname" on line 33. After this, a check ensures the category is valid (a [return of 0](http://codex.wordpress.org/Function_Reference/get_cat_ID#Return_Values) means it's not a valid category) and this allows pages to be created that aren't only titled after categories. Now we know the category is valid, a query can be created and run based on the ID on line 39. A while loop runs through the posts and gathers the content. The next part is copied from content-single.php and it simply formats an excerpt instead of a full post (which is what get_template_part('content', get_post_format()); does, that's what I was using at first). Finally, the comments, footer and other stuff is inserted and the page is complete! To me, the code looks extremely ugly (PHP always does...) with all the open/close tags. But at least it works! Pretty good for a first try...
