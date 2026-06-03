# Combined Transcript — IMG_9549.mov & IMG_9548.mov

## Part 1 (IMG_9549.mov)

Last one, last one. Can you raise your hand? Five, okay. Okay, you guys go ahead and speak up. Make sure you cover first. Hi, I'm Gavin Eber. Hi, my name is Stebby. Hello, my name is Sebastian Novell. Hi guys, okay. We're gonna go real fast. Less talking, I promise.

Okay, so photogrammetry, right? Just raise your hand if anybody in the room knows what photogrammetry is in general. I like that the people in metal rose their hand, that was good. Okay, so photogrammetry, real quick, is you take a bunch of pictures and then you feed it into an ML program and it smartly uses like all the different focal lengths and information that you gather from those pictures and creates a 3D model from it. It kind of became real popular. You know, there's different ways that you could do it. Anyway, that's like the other day. That's like the short version of it.

And so we, as I was talking about, are trying to allow more content to be created faster so we can do more trainings faster. And by doing that, I want to be able to basically take a whole bunch of pictures of my mini fig and then put my mini fig into an application versus me having, because I don't have this model, right? Like this is all Lego. I would have to go and like make the 3D model of this. Well, that's dumb, right? Like that would take forever because this air is ridiculous. So could I take a bunch of pictures of it and then have a smart program make that model for me?

So that exists, right? That's a thing. Part of what we have discovered in doing that, or at least research, we haven't done yet, that's also another longer story, is once that's done, like I can't move that figure's arm up and down necessarily, or have the ability to take like the popsicle out of her hand or take her hair off and things like that. And so that's important if you think about, like I'm taking a picture of a piece of equipment and it has knobs and it has drawers and it has doors and things like move and open, right? I'm teaching somebody how to use equipment. So we want the ability to do the photogrammetry capture, but then be able to interact with that model at the end of the day.

And so, you know, how hard is that? I don't know. What does that process look like? I don't know. It's what you brilliant people in the second row are going to figure out.

So going through the goals, just a pipeline to import photogrammetry models into Unity and then rig those models for interaction. So I gave some different sizes. You like small things. So I'd be interested in like small models, kind of like a medium-sized model, and then like a bigger model because they're all going to be different maybe ways that you think about it from a photogrammetry perspective. And then I'd like the ability to, you know, if it has drawers, if it has knobs, the ability to add that interaction into it.

So at the end of the day, I'm looking just kind of for that MVP of the proof of concept. It doesn't have to be like a full-blown application because this is more like process, like pipeline. But documentation is going to be huge on this one because, you know, you're teaching somebody else, right? It's a train-the-trainer situation. You're going to teach somebody else how to do what you've discovered in such a way that I don't have to come back and ask you a million questions because you've done such a great job of teaching me and documenting it.

We like RealityScan because the software is approved. Again, that's another epic product. We are open to other photogrammetry software options. We have a couple other that are approved, but people haven't really used them that much. And we figured with Epic, it would be easier to import places. But it can't be something that's cloud-based. It all has to be done local on your PC. We use the cloud very sparingly. And so it just would...

## Part 2 (IMG_9548.mov)

We have a couple other that are proof, but people haven't really used them that much. And we figured with Epic it would be easier to import places. But it can't be something that's cloud-based. It all has to be done local on your PC. We use the cloud very sparingly, and so it just would cause a lot of headaches for us. So it needs to be local.

You can take, we prefer something that the pictures, you know, or take it on something like a DSLR. But you can use your phone. You just can't use any of the other, like, if there's special things that your phone can do, like I know iPhones have, like, LiDAR built in. We can't use that, right? It has to just be the image that is being processed.

Okay, that was really as fast as I could go. I don't want two minutes over. Are there any questions that I can go to people?

I think, like, the only question that I'm a little bit confused on is, for this project, is it, are we trying to, like, make it to where we go over, like, the entire process of being able to, like, is it meant to be the program or a thing that we make be able to be worked on multiple different objects? Or is it sort of a object-by-object scenario and we just show the steps on how to get to that point for each object, I guess?

Yeah. I don't need it to be a wizard that I just drop the model in and it automatically does it for me. Like, I don't need it to be that complex. It definitely could be a case-by-case type scenario. That's kind of what I'm expecting. If you are able to automate it in a way, that would be fantastic because that would just make it easier. But the intent at the moment is that this modeling, like the rigging, would be done by people that are XR experts. So kind of our XR development team versus everybody else. The pictures might be taken by novices, but the work would be done by developers, at least at this point. Again, if you can automate it, awesome. But that's not what I'm looking for right now.

Great. Just as a quick overview, you mentioned access to our subject matter experts. So what is your preferred method of communication with the teams in terms of if they have questions, follow-up, but I'm sure they will after today. How should they go through me? Do you want to have them reach out directly and CC me? That kind of thing.

Yeah. I am happy if they want to reach out to me. What I envision, and you can totally change this. I am not trying to take over. Would be, each team would send me a group email with their names and what project they're working on. And of course, CC you every time that they communicate with us. But then, just as ad hoc, they can reach out to us. I'm happy to set up periodic meetings if that's helpful. We try and do that internally with our stakeholders. It's kind of like you have a little mini sprint, and then you're like, here's the thing that I did. Is this still what you want? So that way, everybody kind of feels like, one, I'm getting a progress report. Yay! I feel like stuff is happening. And two, you feel like you're heading in the right direction, especially since I'm not local to Florida. It's hard to have that one-on-one touch time.

So, me, that would be fine, right? I don't know what you guys want to do, but all of that is good to me. And if you guys have other communication methods that work well, that would be good, too. Email is the easiest. We can do Teams. We don't really have the ability to do much other kind of communication, like Discord or anything like that, like officially through work. And so, our preference would be something like Teams or email, just to kind of keep it going. Again, we're no fun. We have zero fun here. So, if it's a fun way to communicate, we probably won't like it. But ask, then we probably won't like it.

Perfect. All right. So, you guys got that. Help the facilitate. Thank you.
