import tkinter as tk
import sys

def cpuschedu():
    win=tk.Tk()
    win.title('CPU SCHEDULING')
    win.geometry('500x500')
    win.configure(bg='skyblue')
    tit=tk.Label(win,text='Simulation of CPU scheduling algorithms',fg='black',bg='yellow',font='Times 16 bold italic')
    tit.pack()
    tk.Label(win,text = 'Project done by:',fg='black',bg='skyblue',font='Times 12 bold italic').pack()
    tk.Label(win,text = 'Balaji - 179X1A02B0',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
    tk.Label(win,text = 'Raman - 179X1A0346',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
    tk.Label(win,text = 'Mahesh - 179X1A03F6',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
    tk.Label(win,bg='skyblue').pack()
    tk.Label(win,text = 'Choose algorithm to simulate:',fg='black',bg='skyblue',font='Times 12 bold italic').pack()
    tk.Label(win,bg='skyblue').pack()
    
    def FCFS():
        
        def sub():
            def clear():
                frame_1.destroy()
            
            arl=list((entry2.get()).split(','))
            arl=[int(i) for i in arl]
            brl=list((entry3.get()).split(','))
            brl=[int(i) for i in brl]
            n=len(arl)
            
            for i in range(n):
                for j in range(i+1,n):
                    if(arl[i] > arl[j]):
                        arl[i],arl[j]=arl[j],arl[i]
                        brl[i],brl[j]=brl[j],brl[i]

            p=['P'+str(i) for i in range(n)] 
            CompletionTime = list()
            TatTime = list()
            CompletionTime.append(arl[0]+brl[0])
            for i in range(1,n):
                CompletionTime.append(brl[i]+CompletionTime[i-1])
            for i in range(0,n):
                TatTime.append(CompletionTime[i]-arl[i])
            waitTime = [TatTime[i]-brl[i] for i in range(n)]

            turn=sum(TatTime)/float(n)
            avg = sum(waitTime)/float(n)
            

            frame_1=tk.LabelFrame(fcfs,text='output parameters',fg='black',bg='skyblue',font='Times 12 bold italic',bd=5,width=250,height=100)
            frame_1.pack(anchor=tk.W)
            

            tk.Label(frame_1,text = "\n----- Ater Performing First Come First Serve Scheduling Algorithm -----\n",fg='black',bg='skyblue',font='Times 13 bold italic').pack(anchor = tk.W)
            
            tk.Label(frame_1,text='  processID  arrival time    burst time  completion time  Turnaround time    waiting time',fg='black',bg='skyblue',font='Times 11 bold italic').pack(anchor=tk.W)
            for i in range(n):
                tk.Label(frame_1,text='     '+str(p[i])+'\t        '+str(arl[i])+'\t\t '+str(brl[i])+'\t  '+str(CompletionTime[i])+'\t\t'+str(TatTime[i])+'\t\t'+str(waitTime[i]),fg='black',bg='skyblue',font='Times 11 bold italic').pack(anchor=tk.W)

            tk.Label(frame_1,text='Average turnaround time -'+str(round(turn,4)),fg='black',bg='skyblue',font='Times 14 bold italic').pack(anchor=tk.W)
            tk.Label(frame_1,text='Average waiting time -'+str(round(avg,4)),fg='black',bg='skyblue',font='Times 14 bold italic').pack(anchor=tk.W)

            tk.Button(frame_1,text='CLEAR OUTPUT',command=clear,width='15',font='Verdana 9 bold',fg='black',bg='light gray',activebackground='green',activeforeground='yellow').pack()

        fcfs=tk.Tk()
        fcfs.title('CPU SCHEDULING')
        fcfs.geometry('565x650')
        fcfs.configure(bg='skyblue')
        tit=tk.Label(fcfs,text='Simulation of CPU scheduling algorithms',fg='black',bg='yellow',font='Times 16 bold italic')
        tit.pack()
        tk.Label(fcfs,text = 'Project done by:',fg='black',bg='skyblue',font='Times 12 bold italic').pack()
        tk.Label(fcfs,text = 'Balaji - 179X1A02B0',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
        tk.Label(fcfs,text = 'Raman - 179X1A0346',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
        tk.Label(fcfs,text = 'Mahesh - 179X1A03F6',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
        
        tk.Label(fcfs,text = '\nFirst Come First Serve\n',fg='black',bg='skyblue',font='Times 12 bold italic').pack()

        frame=tk.LabelFrame(fcfs,text='input parameters',fg='black',bg='skyblue',font='Times 12 bold italic',bd=5,width=250,height=100)
        frame.pack(anchor=tk.W,fill=tk.Y)

        tk.Label(frame,text=' No.of Processes ',fg='black',bg='skyblue',font='Times 10 bold italic').grid(row=0,column=0,sticky=tk.W)
        tk.Label(frame,text=' Arrival Times separated by ,     ',fg='black',bg='skyblue',font='Times 10 bold italic').grid(row=1,column=0,sticky=tk.W)
        tk.Label(frame,text=' Burst Times separated by ,      ',fg='black',bg='skyblue',font='Times 10 bold italic').grid(row=2,column=0,sticky=tk.W)

        entry1=tk.Entry(frame,width=10)
        entry1.insert(0,'3')
        entry1.grid(row=0,column=1)
        entry2=tk.Entry(frame,width=20)
        entry2.insert(0,'0,1,2')
        entry2.grid(row=1,column=1)
        entry3=tk.Entry(frame,width=20)
        entry3.insert(0,'10,2,5')
        entry3.grid(row=2,column=1)

        tk.Label(fcfs,bg='skyblue').pack()

        tk.Button(fcfs,text='SUBMIT',command=sub,width='10',font='Verdana 9 bold',fg='black',bg='light gray',activebackground='green',activeforeground='yellow').pack()
        tk.Label(fcfs,bg='skyblue').pack()
    

    def SJF():
        def sub():
            def clear():
                frame_1.destroy()
            
            arl=list((entry2.get()).split(','))
            arl=[int(i) for i in arl]
            brl=list((entry3.get()).split(','))
            brl=[int(i) for i in brl]
            n=len(arl)
            for i in range(n):
                for j in range(i+1,n):
                    if(arl[i] > arl[j]):
                        arl[i],arl[j]=arl[j],arl[i]
                        brl[i],brl[j]=brl[j],brl[i]
            p=['P'+str(i) for i in range(n)]
            
            pro_data=[]
            for i in range(n):
                te=[]
                te.extend([p[i],arl[i],brl[i],0])
                pro_data.append(te)

            start_time=[]
            exit_time=[]
            s_time=0
            pro_data.sort(key=lambda x:x[1])

            for i in range(n):
                ready_que=[]
                temp=[]
                normal_que=[]
                for j in range(n):
                    if (pro_data[j][1] <= s_time) and (pro_data[j][3] == 0):
                                temp.extend([pro_data[j][0], pro_data[j][1], pro_data[j][2]])
                                ready_que.append(temp)
                                temp = []
                    elif pro_data[j][3] == 0:
                        temp.extend([pro_data[j][0], pro_data[j][1], pro_data[j][2]])
                        normal_que.append(temp)
                        temp = []
                
                if(len(ready_que) != 0):
                    ready_que.sort(key=lambda x: x[2])

                    start_time.append(s_time)
                    s_time = s_time + ready_que[0][2]
                    e_time = s_time
                    exit_time.append(e_time)
                    for k in range(len(pro_data)):
                        if pro_data[k][0] == ready_que[0][0]:
                            break
                    pro_data[k][3] = 1
                    pro_data[k].append(e_time)

                elif(len(ready_que) == 0):
                    if s_time < normal_que[0][1]:
                        s_time = normal_que[0][1]
                    start_time.append(s_time)
                    s_time = s_time + normal_que[0][2]
                    e_time = s_time
                    exit_time.append(e_time)
                    for k in range(len(pro_data)):
                        if pro_data[k][0] == normal_que[0][0]:
                            break
                    pro_data[k][3] = 1
                    pro_data[k].append(e_time)

            

            total_turnaround_time=0
            for i in range(n):
                turnaround_time = pro_data[i][4] - pro_data[i][1]
                total_turnaround_time = total_turnaround_time + turnaround_time
                pro_data[i].append(turnaround_time)
            turn=total_turnaround_time/float(n)
            total_waiting_time = 0
            for i in range(len(pro_data)):
                waiting_time = pro_data[i][5] - pro_data[i][2]
                total_waiting_time = total_waiting_time + waiting_time
                pro_data[i].append(waiting_time)
            avg = total_waiting_time / float(n)

            pro_data.sort(key=lambda x: x[0]) 
            

            frame_1=tk.LabelFrame(sjf,text='output parameters',fg='black',bg='skyblue',font='Times 12 bold italic',bd=5,width=250,height=100)
            frame_1.pack(anchor=tk.W)
            

            tk.Label(frame_1,text = "\n----- Ater Performing Shortest Job First Scheduling Algorithm -----\n",fg='black',bg='skyblue',font='Times 13 bold italic').pack(anchor = tk.W)
            
            tk.Label(frame_1,text='  processID  arrival time    burst time  completion time  Turnaround time    waiting time',fg='black',bg='skyblue',font='Times 11 bold italic').pack(anchor=tk.W)
            for i in range(n):
                
                tk.Label(frame_1,text='     '+str(pro_data[i][0])+'\t        '+str(pro_data[i][1])+'\t\t '+str(pro_data[i][2])+'\t  '+str(pro_data[i][4])+'\t\t'+str(pro_data[i][5])+'\t\t'+str(pro_data[i][6]),fg='black',bg='skyblue',font='Times 11 bold italic').pack(anchor=tk.W)

            tk.Label(frame_1,text='Average turnaround time -'+str(round(turn,4)),fg='black',bg='skyblue',font='Times 14 bold italic').pack(anchor=tk.W)
            tk.Label(frame_1,text='Average waiting time -'+str(round(avg,4)),fg='black',bg='skyblue',font='Times 14 bold italic').pack(anchor=tk.W)

            tk.Button(frame_1,text='CLEAR OUTPUT',command=clear,width='15',font='Verdana 9 bold',fg='black',bg='light gray',activebackground='green',activeforeground='yellow').pack()

        sjf=tk.Tk()
        sjf.title('CPU SCHEDULING')
        sjf.geometry('565x670')
        sjf.configure(bg='skyblue')
        tit=tk.Label(sjf,text='Simulation of CPU scheduling algorithms',fg='black',bg='yellow',font='Times 16 bold italic')
        tit.pack()
        tk.Label(sjf,text = 'Project done by:',fg='black',bg='skyblue',font='Times 12 bold italic').pack()
        tk.Label(sjf,text = 'Balaji - 179X1A02B0',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
        tk.Label(sjf,text = 'Raman - 179X1A0346',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
        tk.Label(sjf,text = 'Mahesh - 179X1A03F6',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
        
        tk.Label(sjf,text = '\nShortest Job First\n',fg='black',bg='skyblue',font='Times 12 bold italic').pack()

        frame=tk.LabelFrame(sjf,text='input parameters',fg='black',bg='skyblue',font='Times 12 bold italic',bd=5,width=250,height=100)
        frame.pack(anchor=tk.W,fill=tk.Y)

        tk.Label(frame,text=' No.of Processes ',fg='black',bg='skyblue',font='Times 10 bold italic').grid(row=0,column=0,sticky=tk.W)
        tk.Label(frame,text=' Arrival Times separated by ,     ',fg='black',bg='skyblue',font='Times 10 bold italic').grid(row=1,column=0,sticky=tk.W)
        tk.Label(frame,text=' Burst Times separated by ,      ',fg='black',bg='skyblue',font='Times 10 bold italic').grid(row=2,column=0,sticky=tk.W)

        entry1=tk.Entry(frame,width=10)
        entry1.insert(0,'3')
        entry1.grid(row=0,column=1)
        entry2=tk.Entry(frame,width=20)
        entry2.insert(0,'0,1,2')
        entry2.grid(row=1,column=1)
        entry3=tk.Entry(frame,width=20)
        entry3.insert(0,'10,2,5')
        entry3.grid(row=2,column=1)

        tk.Label(sjf,bg='skyblue').pack()

        tk.Button(sjf,text='SUBMIT',command=sub,width='10',font='Verdana 9 bold',fg='black',bg='light gray',activebackground='green',activeforeground='yellow').pack()
        tk.Label(sjf,bg='skyblue').pack()
    def PB():
        def sub():
            def clear():
                frame_1.destroy()
            
            arl=list((entry2.get()).split(','))
            arl=[int(i) for i in arl]
            brl=list((entry3.get()).split(','))
            brl=[int(i) for i in brl]
            pri=list((entry4.get()).split(','))
            pri=[int(i) for i in pri]
            n=len(arl)
            
            for i in range(n):
                for j in range(i+1,n):
                    if(arl[i]>arl[j]):
                        arl[i],arl[j]=arl[j],arl[i]
                        brl[i],brl[j]=brl[j],brl[i]
                        pri[i],pri[j]=pri[j],pri[i]

            p=['P'+str(i) for i in range(n)]
            
            pro_data=[]
            for i in range(n):
                te=[]
                te.extend([p[i],arl[i],brl[i],pri[i],0])
                pro_data.append(te)

            start_time = []
            exit_time = []
            s_time = 0
            pro_data.sort(key=lambda x: x[1])
            
            for i in range(len(pro_data)):
                ready_queue = []
                temp = []
                normal_queue = []
                for j in range(len(pro_data)):
                    if (pro_data[j][1] <= s_time) and (pro_data[j][4] == 0):
                        temp.extend([pro_data[j][0], pro_data[j][1], pro_data[j][2], pro_data[j][3]])
                        ready_queue.append(temp)
                        temp = []
                    elif pro_data[j][4] == 0:
                        temp.extend([pro_data[j][0], pro_data[j][1], pro_data[j][2], pro_data[j][3]])
                        normal_queue.append(temp)
                        temp = []
                if len(ready_queue) != 0:
                    ready_queue.sort(key=lambda x: x[3], reverse=True)
                    start_time.append(s_time)
                    s_time = s_time + ready_queue[0][2]
                    e_time = s_time
                    exit_time.append(e_time)
                    for k in range(len(pro_data)):
                        if pro_data[k][0] == ready_queue[0][0]:
                            break
                    pro_data[k][4] = 1
                    pro_data[k].append(e_time)
                elif len(ready_queue) == 0:
                    if s_time < normal_queue[0][1]:
                        s_time = normal_queue[0][1]
                    start_time.append(s_time)
                    s_time = s_time + normal_queue[0][2]
                    e_time = s_time
                    exit_time.append(e_time)
                    for k in range(len(pro_data)):
                        if pro_data[k][0] == normal_queue[0][0]:
                            break
                    pro_data[k][4] = 1
                    pro_data[k].append(e_time)
            
            total_turnaround_time=0
            for i in range(n):
                turnaround_time = pro_data[i][5] - pro_data[i][1]
                total_turnaround_time = total_turnaround_time + turnaround_time
                pro_data[i].append(turnaround_time)
            turn=total_turnaround_time/float(n)

            total_waiting_time = 0
            for i in range(len(pro_data)):
                waiting_time = pro_data[i][6] - pro_data[i][2]
                total_waiting_time = total_waiting_time + waiting_time
                pro_data[i].append(waiting_time)
            avg = total_waiting_time / float(n)

            pro_data.sort(key=lambda x: x[0]) 


            frame_1=tk.LabelFrame(pb,text='output parameters',fg='black',bg='skyblue',font='Times 12 bold italic',bd=5,width=250,height=100)
            frame_1.pack(anchor=tk.W)
            

            tk.Label(frame_1,text = "\n----- Ater Performing Priority based Scheduling Algorithm -----\n",fg='black',bg='skyblue',font='Times 13 bold italic').pack(anchor = tk.W)
            
            tk.Label(frame_1,text='  processID  arrival time    burst time   priority  completion time  Turnaround time      waiting time',fg='black',bg='skyblue',font='Times 11 bold italic').pack(anchor=tk.W)

            for i in range(n):
                tk.Label(frame_1,text='     '+str(pro_data[i][0])+'\t        '+str(pro_data[i][1])+'\t\t '+str(pro_data[i][2])+'\t   '+str(pro_data[i][3])+'\t '+str(pro_data[i][5])+'\t\t'+str(pro_data[i][6])+'\t\t'+str(pro_data[i][7]),fg='black',bg='skyblue',font='Times 11 bold italic').pack(anchor=tk.W)

            tk.Label(frame_1,text='Average turnaround time -'+str(round(turn,4)),fg='black',bg='skyblue',font='Times 14 bold italic').pack(anchor=tk.W)
            tk.Label(frame_1,text='Average waiting time -'+str(round(avg,4)),fg='black',bg='skyblue',font='Times 14 bold italic').pack(anchor=tk.W)

            tk.Button(frame_1,text='CLEAR OUTPUT',command=clear,width='15',font='Verdana 9 bold',fg='black',bg='light gray',activebackground='green',activeforeground='yellow').pack()

        pb=tk.Tk()
        pb.title('CPU SCHEDULING')
        pb.geometry('630x670')
        pb.configure(bg='skyblue')
        tit=tk.Label(pb,text='Simulation of CPU scheduling algorithms',fg='black',bg='yellow',font='Times 16 bold italic')
        tit.pack()
        tk.Label(pb,text = 'Project done by:',fg='black',bg='skyblue',font='Times 12 bold italic').pack()
        tk.Label(pb,text = 'Balaji - 179X1A02B0',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
        tk.Label(pb,text = 'Raman - 179X1A0346',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
        tk.Label(pb,text = 'Mahesh - 179X1A03F6',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
        
        tk.Label(pb,text = '\nPriority Based Scheduling\n',fg='black',bg='skyblue',font='Times 12 bold italic').pack()

        frame=tk.LabelFrame(pb,text='input parameters',fg='black',bg='skyblue',font='Times 12 bold italic',bd=5,width=250,height=100)
        frame.pack(anchor=tk.W,fill=tk.Y)

        tk.Label(frame,text=' No.of Processes ',fg='black',bg='skyblue',font='Times 10 bold italic').grid(row=0,column=0,sticky=tk.W)
        tk.Label(frame,text=' Arrival Times separated by ,     ',fg='black',bg='skyblue',font='Times 10 bold italic').grid(row=1,column=0,sticky=tk.W)
        tk.Label(frame,text=' Burst Times separated by ,      ',fg='black',bg='skyblue',font='Times 10 bold italic').grid(row=2,column=0,sticky=tk.W)
        tk.Label(frame,text=' Priorities separated by , ',fg='black',bg='skyblue',font='Times 10 bold italic').grid(row=3,column=0,sticky=tk.W)

        entry1=tk.Entry(frame,width=10)
        entry1.insert(0,'3')
        entry1.grid(row=0,column=1)
        entry2=tk.Entry(frame,width=20)
        entry2.insert(0,'0,1,2')
        entry2.grid(row=1,column=1)
        entry3=tk.Entry(frame,width=20)
        entry3.insert(0,'10,2,5')
        entry3.grid(row=2,column=1)
        entry4=tk.Entry(frame,width=20)
        entry4.insert(0,'1,2,3')
        entry4.grid(row=3,column=1)

        tk.Label(pb,bg='skyblue').pack()

        tk.Button(pb,text='SUBMIT',command=sub,width='10',font='Verdana 9 bold',fg='black',bg='light gray',activebackground='green',activeforeground='yellow').pack()
        tk.Label(pb,bg='skyblue').pack()
    def RR():
        def sub():
            def clear():
                frame_1.destroy()
            t=int(entry4.get())
            arl=list((entry2.get()).split(','))
            arl=[int(i) for i in arl]
            brl=list((entry3.get()).split(','))
            brl=[int(i) for i in brl]
            n=len(arl)
            for i in range(n):
                for j in range(i+1,n):
                    if(arl[i] > arl[j]):
                        arl[i],arl[j]=arl[j],arl[i]
                        brl[i],brl[j]=brl[j],brl[i]
            
            p=['P'+str(i) for i in range(n)]

            pro_data=[]
            for i in range(n):
                te=[]
                te.extend([p[i],arl[i],brl[i],0,brl[i]])
                pro_data.append(te)

            start_time=[]
            exit_time=[]
            executed_pro=[]
            ready_que=[]
            s_time=0
            pro_data.sort(key=lambda x:x[1])
            
            time_slice=t
            
            while 1:
                normal_que = []
                temp = []
                for i in range(len(pro_data)):
                    if pro_data[i][1] <= s_time and pro_data[i][3] == 0:
                        present = 0
                        if len(ready_que) != 0:
                            for k in range(len(ready_que)):
                                if pro_data[i][0] == ready_que[k][0]:
                                    present = 1
                        
                        if present == 0:
                            temp.extend([pro_data[i][0], pro_data[i][1], pro_data[i][2], pro_data[i][4]])
                            ready_que.append(temp)
                            temp = []
                        
                        if len(ready_que) != 0 and len(executed_pro) != 0:
                            for k in range(len(ready_que)):
                                if ready_que[k][0] == executed_pro[len(executed_pro) - 1]:
                                    ready_que.insert((len(ready_que) - 1), ready_que.pop(k))
                        
                    elif pro_data[i][3] == 0:
                        temp.extend([pro_data[i][0], pro_data[i][1], pro_data[i][2], pro_data[i][4]])
                        normal_que.append(temp)
                        temp = []
                if len(ready_que) == 0 and len(normal_que) == 0:
                    break
                if len(ready_que) != 0:
                    if ready_que[0][2] > time_slice:
                        start_time.append(s_time)
                        s_time = s_time + time_slice
                        e_time = s_time
                        exit_time.append(e_time)
                        executed_pro.append(ready_que[0][0])
                        for j in range(len(pro_data)):
                            if pro_data[j][0] == ready_que[0][0]:
                                break
                        pro_data[j][2] = pro_data[j][2] - time_slice
                        ready_que.pop(0)
                    elif ready_que[0][2] <= time_slice:
                        start_time.append(s_time)
                        s_time = s_time + ready_que[0][2]
                        e_time = s_time
                        exit_time.append(e_time)
                        executed_pro.append(ready_que[0][0])
                        for j in range(len(pro_data)):
                            if pro_data[j][0] == ready_que[0][0]:
                                break
                        pro_data[j][2] = 0
                        pro_data[j][3] = 1
                        pro_data[j].append(e_time)
                        ready_que.pop(0)
                elif len(ready_que) == 0:
                    if s_time < normal_que[0][1]:
                        s_time = normal_que[0][1]
                    if normal_que[0][2] > time_slice:
                        start_time.append(s_time)
                        s_time = s_time + time_slice
                        e_time = s_time
                        exit_time.append(e_time)
                        executed_pro.append(normal_que[0][0])
                        for j in range(len(pro_data)):
                            if pro_data[j][0] == normal_que[0][0]:
                                break
                        pro_data[j][2] = pro_data[j][2] - time_slice
                    elif normal_que[0][2] <= time_slice:
                        start_time.append(s_time)
                        s_time = s_time + normal_que[0][2]
                        e_time = s_time
                        exit_time.append(e_time)
                        executed_pro.append(normal_que[0][0])
                        for j in range(len(pro_data)):
                            if pro_data[j][0] == normal_que[0][0]:
                                break
                        pro_data[j][2] = 0
                        pro_data[j][3] = 1
                        pro_data[j].append(e_time)
            

            total_turnaround_time=0
            for i in range(n):
                turnaround_time = pro_data[i][5] - pro_data[i][1]
                total_turnaround_time = total_turnaround_time + turnaround_time
                pro_data[i].append(turnaround_time)
            turn=total_turnaround_time/float(n)
            total_waiting_time = 0
            for i in range(len(pro_data)):
                waiting_time = pro_data[i][6] - pro_data[i][4]
                total_waiting_time = total_waiting_time + waiting_time
                pro_data[i].append(waiting_time)
            avg = total_waiting_time / float(n)

            pro_data.sort(key=lambda x: x[0]) 
            

            frame_1=tk.LabelFrame(rrb,text='output parameters',fg='black',bg='skyblue',font='Times 12 bold italic',bd=5,width=250,height=100)
            frame_1.pack(anchor=tk.W)
            

            tk.Label(frame_1,text = "\n----- Ater Performing Round Robin Scheduling Algorithm -----\n",fg='black',bg='skyblue',font='Times 13 bold italic').pack(anchor = tk.W)
            
            tk.Label(frame_1,text='  processID  arrival time    burst time  completion time  Turnaround time    waiting time',fg='black',bg='skyblue',font='Times 11 bold italic').pack(anchor=tk.W)
            for i in range(n):
                
                tk.Label(frame_1,text='     '+str(pro_data[i][0])+'\t        '+str(pro_data[i][1])+'\t\t '+str(pro_data[i][4])+'\t  '+str(pro_data[i][5])+'\t\t'+str(pro_data[i][6])+'\t\t'+str(pro_data[i][7]),fg='black',bg='skyblue',font='Times 11 bold italic').pack(anchor=tk.W)

            tk.Label(frame_1,text='Average turnaround time -'+str(round(turn,4)),fg='black',bg='skyblue',font='Times 14 bold italic').pack(anchor=tk.W)
            tk.Label(frame_1,text='Average waiting time -'+str(round(avg,4)),fg='black',bg='skyblue',font='Times 14 bold italic').pack(anchor=tk.W)

            tk.Button(frame_1,text='CLEAR OUTPUT',command=clear,width='15',font='Verdana 9 bold',fg='black',bg='light gray',activebackground='green',activeforeground='yellow').pack()

        rrb=tk.Tk()
        rrb.title('CPU SCHEDULING')
        rrb.geometry('565x650')
        rrb.configure(bg='skyblue')
        tit=tk.Label(rrb,text='Simulation of CPU scheduling algorithms',fg='black',bg='yellow',font='Times 16 bold italic')
        tit.pack()
        tk.Label(rrb,text = 'Project done by:',fg='black',bg='skyblue',font='Times 12 bold italic').pack()
        tk.Label(rrb,text = 'Balaji - 179X1A02B0',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
        tk.Label(rrb,text = 'Raman - 179X1A0346',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
        tk.Label(rrb,text = 'Mahesh - 179X1A03F6',fg='black',bg='skyblue',font='Times 10 bold italic').pack()
        
        tk.Label(rrb,text = '\nRound Robin Scheduling\n',fg='black',bg='skyblue',font='Times 12 bold italic').pack()

        frame=tk.LabelFrame(rrb,text='input parameters',fg='black',bg='skyblue',font='Times 12 bold italic',bd=5,width=250,height=100)
        frame.pack(anchor=tk.W,fill=tk.Y)

        tk.Label(frame,text=' No.of Processes ',fg='black',bg='skyblue',font='Times 10 bold italic').grid(row=0,column=0,sticky=tk.W)
        tk.Label(frame,text=' Arrival Times separated by ,     ',fg='black',bg='skyblue',font='Times 10 bold italic').grid(row=2,column=0,sticky=tk.W)
        tk.Label(frame,text=' Burst Times separated by ,      ',fg='black',bg='skyblue',font='Times 10 bold italic').grid(row=3,column=0,sticky=tk.W)
        tk.Label(frame,text=' Time Quantum ,      ',fg='black',bg='skyblue',font='Times 10 bold italic').grid(row=1,column=0,sticky=tk.W)

        entry1=tk.Entry(frame,width=10)
        entry1.insert(0,'3')
        entry1.grid(row=0,column=1)
        entry2=tk.Entry(frame,width=20)
        entry2.insert(0,'0,1,2')
        entry2.grid(row=2,column=1)
        entry3=tk.Entry(frame,width=20)
        entry3.insert(0,'10,2,5')
        entry3.grid(row=3,column=1)
        entry4=tk.Entry(frame,width=10)
        entry4.insert(0,'2')
        entry4.grid(row=1,column=1)

        tk.Label(rrb,bg='skyblue').pack()

        tk.Button(rrb,text='SUBMIT',command=sub,width='10',font='Verdana 9 bold',fg='black',bg='light gray',activebackground='green',activeforeground='yellow').pack()
        tk.Label(rrb,bg='skyblue').pack()
    def quit():
        sys.exit()

    tk.Button(win,text='First Come First Serve(FCFS)',command=FCFS,width='27',font='Verdana 9 bold',fg='black',bg='light gray',activebackground='green',activeforeground='yellow').pack()
    tk.Label(win,bg='skyblue').pack()
    tk.Button(win,text='Shortest Job First(SJF)',command=SJF,width='27',font='Verdana 9 bold',fg='black',bg='light gray',activebackground='green',activeforeground='yellow').pack()
    tk.Label(win,bg='skyblue').pack()
    tk.Button(win,text='Priority Based Scheduling',command=PB,width='27',font='Verdana 9 bold',fg='black',bg='light gray',activebackground='green',activeforeground='yellow').pack()
    tk.Label(win,bg='skyblue').pack()
    tk.Button(win,text='Round Robin Scheduling',command=RR,width='27',font='Verdana 9 bold',fg='black',bg='light gray',activebackground='green',activeforeground='yellow').pack()
    tk.Label(win,bg='skyblue').pack()
    tk.Button(win,text='Quit',command=quit,width='10',font='Verdana 9 bold',fg='black',bg='light gray',activebackground='green',activeforeground='yellow').pack()
    

    win.mainloop()


if __name__=="__main__":
    cpuschedu()
