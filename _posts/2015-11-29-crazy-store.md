---
layout: post
title: Making a Crazy Store

---

Coming to the end of my rails track at Bloc, I have been tasked with making a capstone project. I came up with an idea for a store where a user could sell something that isn't theirs - for a profit. Bear with me if this sounds crazy, for I shall paint you, my dear reader, a picture. 

You are travelling in Costa Rica. You come across a shop that sells signature custom made wooden bowls by the side of the road. You are amazed at the product, but even more amazed at the price, say, $45. You see things like this sell for hundreds of dollars in the US. So you decide to *Snap and Move*. You take a picture, with a quick description of the object. In one click you list it on the store with a price you set, say $300. A few weeks later you see that $240 dollars has been deposited into your Snap and Move Account, available for transfer to any bank of your choosing. 

That sounds great, doesn't it? In fact, taking the idea to an extreme, you could theoretically subsidize entire trips using the store. So there, that was the idea. 

I set out to implement it with rails. I did basic rails scaffolding for Users, Items, and Orders, and used stripe to implement payment. 

I had a bit of trouble executing certain features such as searching and sorting lists of items and users. I solved my problem like this:

I made a method I could call in the view to make something sortable. 

{%highlight ruby%}
module ApplicationHelper
	def sortable(column, title = nil)
		title ||=column.titleize
		direction = column == sort_column && sort_direction == "ASC" ? "DESC" : "ASC"
		link_to title, :sort => column, :direction => direction
	end
end
{%endhighlight%}

In the Items Controller

{%highlight ruby%}

def index
    if params[:search]
      @items = Item.search(params[:search]).order("created_at DESC").paginate(:page => params[:page], :per_page => 10)
    elsif params[:sort]
      @items = Item.all.reorder(sort_column + " " + sort_direction).paginate(:page => params[:page], :per_page => 10)
    else params[:page]
      @items = Item.paginate(:page => params[:page], :per_page => 10)
    end
  end

 private

  def sort_column
    Item.column_names.include?(params[:sort]) ? params[:sort] : "title"
  end
  
  def sort_direction
    %w[ASC DESC].include?(params[:direction]) ? params[:direction] : "asc"
  end
{%endhighlight%}

I found that by passing in a sort param, I could call the sort and make it reversable by pressing the button again. 

What is the magic behind actually getting orders completed?

Fulfillers.

I made fulfillers a class of user that could log in, and fulfill orders in their area by reading from a list, collecting the order with money from the store, and then taking some sort of fee for themselves. The fulfiller view looks like this:

![Geometric pattern with fading gradient]({{ site.baseurl }}/img/tehstore.png)

When orders are updated, I use Mailgun as well as a notification system to notify buyers and sellers of what's going on. This store has a lot of progress to go before it is ready, but I am proud of what I have done so far. Check out the code on my GitHub [here](https://github.com/occamskatana/tehstore).
