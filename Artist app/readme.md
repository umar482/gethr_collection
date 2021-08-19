Shahab and Umar are building this

the data for campaign architecture is in the campaigns prod- dynamoDB

1. create customer and store in customers table (script exists).
2.  create campaignSongsData.json and manually add name campaign, set start date, auto length is 3-6 weeks (determined by streamer matches and stream frequency).
3. for song 1 add spotify url (extract song_id) and upload mp3 and link with song_id
4. run song 1 through musiio api and get tags add to campaignSongsData.json
5. run the info through the spotify api get the info (existing function addSongMetaData already does this in add-quick-campaign.py).
6.  run song 1 data from campaignSongsData.json through the models for each of the streamers to generate a score for each streamer (federico) of how good a match it is for them and add to the streamer-song-score table.
7. then repeat 3-6 for the rest of the songs in the campaign,
8.  create a script that matches songs with a streamer such that, the spend is just over budget just before 6 weeks. while maintaining the highest possible average score. Ie start with the best match song (highest score for a streamer) across all the songs in the campaign. calculate the expended spend, do the next highest and then next highest, until the budget is hit. If hitting the budget requires putting a song with a below a .5, but above a .35 send a warning slack message to a campaigns channel. but include it campaign. but if below a .35, don't include it.  That data should be added to the campaignInfoImport.json (ask massey).
9. run add-quick-campaign.py ( minus the spotifyMetaData function)
