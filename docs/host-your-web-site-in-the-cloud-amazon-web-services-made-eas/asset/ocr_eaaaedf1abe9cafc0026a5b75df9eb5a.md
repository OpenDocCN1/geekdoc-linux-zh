replace the existing ones, or **horizontal scaling**, where additional servers are placed side-by-side (architecturally speaking) with the existing resources. Vertical scaling is sometimes called a scale-up model, and horizontal scaling is sometimes called a scale-out model.

# ## Vertical Scaling

At first, vertical scaling appears to be the easiest way to add capacity. You start out with a server of modest means and use it until it no longer meets your needs. You purchase a bigger one, move your code and data over to it, and abandon the old one. Performance is good until the newer, larger system reaches its capacity. You purchase again, repeating the process until your hardware supplier informs you that you’re running on the largest hardware that they have, and that you’ve no more room to grow. At this point you’ve effectively painted yourself into a corner.

Vertical scaling can be expensive. Each time you upgrade to a bigger system you also make a correspondingly larger investment. If you’re actually buying hardware, your first step-ups cost you thousands of dollars; your later ones cost you tens or even hundreds of thousands of dollars. At some point you may have to invest in a similarly expensive backup system, which will remain idle unless the unthinkable happens and you need to use it to continue operations.

# ## Horizontal Scaling

Horizontal scaling is slightly more complex, but far more flexible and scalable in the long term. Instead of upgrading to a bigger server, you obtain another one (presumably of the same size, although there’s no requirement for this to be the case) and arrange to share the storage and processing load across two servers. When two servers no longer meet your needs, you add a third, a fourth, and so on. This scale-out model allows you to add resources incrementally and economically. As your fleet of servers grow, you can actually increase the reliability of your system by eliminating dependencies on any particular server.

Of course, sharing the storage and processing load across a fleet of servers is sometimes easier said than done. Loosely coupled systems tied together with SQS message queues like those we saw and built in the previous chapter can usually scale easily. Systems with a reliance on a traditional relational database or another centralized storage can be more difficult.