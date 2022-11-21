# write-a-triggrt-on-Opportunity-fields-if-stage-closed-Won-you-cannot-upd
write a triggr on Opportunity fields if stage =closed Won you cannot update the record
trigger beforeUpdateTrigger on Opportunity (after update,before update)
{
    if((trigger.isafter && trigger.isupdate)||(trigger.isbefore && trigger.isupdate))
        
    {
        myaccountHandlers.mymethods(trigger.New,trigger.oldmap);
    }
    
    
}
   

public class myaccountHandlers 
{
     public static void mymethods(list<opportunity>opplist,map<id,opportunity>oppmap)
     {
        for(opportunity app:opplist)
        { 
            opportunity  ooppsce=oppmap.get(app.Id);   //frist ftach old record field value 
            if(app.StageName=='closed Won' || (ooppsce.StageName=='closed Won' &&  app.StageName !=ooppsce.StageName)) 
                  //then compare old value and new value
            {  //frist if staggename =closed won when record insert
                //OR old record closed won and new stagename not equal to closed won then this loop wxecuted
                app.addError('hey you cannot update Now');
            }
        }
     }

}
