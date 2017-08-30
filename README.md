# NeptuneLiveBusyDialog
Live Busy Dialog utility for use with SAP, Neptune and ABAP Messaging Channels

Background
When starting to develop in Neptune, I came to find that I really missed the good old cl_progress_indicator (or FM sapgui_progress_indicator). All there was available was the oApp.setBusy() and the sap.m.BusyDialog control. By all means, this is for many cases good enough. We do not want the user to be kept waiting anyways and we generally do not really build the kind of heavy report apps that need this to the same extent as we tend to have made in the SAP GUI. But then again, sometimes we do need to provide additional information for a good user experience.

So when developing a specific offline app where quite a lot of data is reported back into the backend and different business processes take their due time, I thought the issue needed to be addressed and now I put it in the hands of the community. I was partly influenced by Aleksander Domalewski's "Move from pull to push methodology via ABAP Channels and Neptune Software". Please check that out as well.


The thought and idea
The basic idea is that the frontend is locked (busy) during the processing of the entire AJAX call in the backend, as usual. During this time, progress information is pushed to an ABAP Channel in the backend and caught in a WebSocket in the frontend with JavaScript to present/update this information to the user.

Since the backend is stateless and we may have several instances of the same app running, I generate a sort of UUID that is "unique enough" for these purposes. The UUID is sent to the backend with the AJAX call and kept globally in the frontend to identify the corresponding messages to display/update.

Since I may want to reuse this same solution for several apps in the same system, and eailly port this to other systems, I create a "utility class" for the types and methods for connection and pushing of messages.


My solution
I present you my solution with some remarks as of my thinking. I assume that if you are part of this community and want to use this, you are familiar with both ABAP development for the backend and NAD for the frontend, so i will not go into deep technical detail of every step of the process for you. 
