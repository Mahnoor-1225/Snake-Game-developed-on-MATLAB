# Snake-Game-developed-on-MATLAB
#This is a snake game developed on MATLAB. It is its MALTAB file developed for the changing and access of its code and work.
Properties code:
dir=0;
score=0;
function code:
dim = 16;
            app.score = 0;
            app.dir = 0;
            cla(app.UIAxes)
           
            v = 0.9;
            f = [0 0];
            f(1) = round(rand*dim);
            f(2) = round(rand*dim);         
            s = zeros(100,2);
            s_old = zeros (100,2);
            s(1,1) = round(dim/2);
            s(1,2) = round(dim/2);            
            s(2,1) = 5;
            s(2,2) = 6;
            snake = plot(app.UIAxes,s([1 2],1),s([1 2],2),'Marker','.','MarkerSize',20,'LineStyle','-','LineWidth',10,'Color','#4CCB32');
            hold(app.UIAxes,'on');
            food = plot(app.UIAxes,f(1,1),f(1,2),'Marker','.','MarkerSize',30,'MarkerFaceColor','r','LineStyle','-','LineWidth',10);
            
            xlim(app.UIAxes,[0 20])
            ylim(app.UIAxes,[0 20])
            
            while (1)
                id = 0;
                s_old = s;
                
                %Update Head Position
                if(app.dir==0)
                    s(1,1)=s_old(1,1)-1;
                    s(1,2)=s_old(1,2);
                elseif(app.dir==1)
                    s(1,1)=s_old(1,1);
                    s(1,2)=s_old(1,2)+1;
                elseif(app.dir==2)
                    s(1,1)=s_old(1,1)+1;
                    s(1,2)=s_old(1,2);
                elseif(app.dir==3)
                    s(1,1)=s_old(1,1);
                    s(1,2)=s_old(1,2)-1;
                end
                
                %Update Body Position
                
                for i=2:1:length(nonzeros(s(:,1)))
                    s(i,1) = s_old(i-1,1);
                    s(i,2) = s_old(i-1,2);
                end
                
                %Limit area
                
                if(s(1,1)>dim||s(1,1)<0||s(1,2)>dim||s(1,2)<0)
                    msgbox(strcat('Out of the limits, game ended! Score: ',int2str(app.score)),'End');
                    break
                end
                
                %Touch body
                
                if(isempty(find(prod(s(1,1:2)==s(2:end,1:2),2)))==0)
                    msgbox(strcat('Out of the limits, game ended! Score: ',int2str(app.score)),'End');
                    break
                end
                
                %Eating
                
                if(s(1,[1 2])==f)
                    s(length(nonzeros(s(:,1)))+1,1) = s_old(length(nonzeros(s_old(:,1))),1);
                    s(length(nonzeros(s(:,2)))+1,2) = s_old(length(nonzeros(s_old(:,2))),2);
                    f(1) = round(rand*dim);
                    f(2) = round(rand*dim);
                    app.score = app.score+1;
                    v = v-0.02;
                end
                
                %Plotting
                
                app.ScoreEditField.Value= int2str(app.score);
                set(snake,'XData',nonzeros(s(:,1)),'YData',nonzeros(s(:,2)));
                set(food,'XData',nonzeros(f(:,1)),'YData',nonzeros(f(:,2)));
                pause(v)
            end
callback code:
key = event.Key;
            if(strcmp(key,'leftarrow') && app.dir ~= 2 )
                app.dir=0;
            end
            if(strcmp(key,'rightarrow') && app.dir ~= 0 )
                app.dir=2;
            end
            if(strcmp(key,'uparrow') && app.dir ~= 3 )
                app.dir=1;
            end
            if(strcmp(key,'downarrow') && app.dir ~= 1 )
                app.dir=3;
            end
