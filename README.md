# TableReloadingNotifier
A sample project which provides how to notify when the table view has finished loading.


I have created this project as this stackoverflow post was getting lot of views
http://stackoverflow.com/questions/1483581/get-notified-when-uitableview-has-finished-asking-for-data/21581834#21581834

This is just a proof of concept for the answer i have provided in the post.

Solution
========
Though tableview provides a lot of delegates by default there is no delegate to intimate when the tableview has actually finished loading. 
The solution would be to use the GCD after the tableview.reload is called

        self.tableView.reloadData()
        dispatch_async(dispatch_get_main_queue(), { () -> Void in
            print("Reload Finished after cells are crated");
        })

 
How this works
==============

Basically when you do a reload the main thread becomes busy so at that time when we do a dispatch async thread, the block will wait till the main thread gets finished. So once the tableview has been loaded completely the main thread will gets finish and so it will dispatch our method block

Tested Environments
===================

iOS7, iOS8 and iOS9

Screenshots
===========
Screenshot taken in iOS9 iPhone6 simulator from Xcode7

![](https://raw.githubusercontent.com/ipraba/TableReloadingNotifier/master/Screenshots/Screen%20Shot%202015-10-30%20at%208.58.24%20am.png)

![](https://raw.githubusercontent.com/ipraba/TableReloadingNotifier/master/Screenshots/Simulator%20Screen%20Shot%2030-Oct-2015%208.53.43%20am.png)


