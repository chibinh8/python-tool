#Binh Le Chi - RBVH
#Auto Rename utility
import sys, re, os, stat

#match and fit the string with template
def write_vartofile(file,line_to_write,list_vardetected,component):
    line_to_write=line_to_write.replace(r'(',r' ')
    line_to_write=line_to_write.replace(r')',r' ')
    line_to_write=line_to_write.replace(r'}',r' ')
    line_to_write=line_to_write.replace(r'{',r' ')
    line_to_write=line_to_write.replace(r'!',r' ')
    line_to_write=line_to_write.replace(r';',r' ')
    line_to_write=line_to_write.replace(r'=',r' = ')
    list_vardetected=re.sub(r'\=.*$','',list_vardetected,)
    line_replaced=''
    #debug
    if(list_vardetected==r'VDB_S_GetVidObjDxvTC_sw'):
        bl=1
    print(list_vardetected)
    print(line_to_write)
    if line_to_write.count(r'[')==0:
        if line_to_write.count(r'=')>0:
         pattern_line_w=re.compile(r'^.*\W('+re.escape(component)+r'.*_)(pst->|st\.)(\S+)\s+\=.*;*',re.I)
        else:
         pattern_line_w=re.compile(r'^.*\W('+re.escape(component)+r'.*_)(pst->|st\.)(\S+).*;*',re.I)
        if(pattern_line_w.search(line_to_write)!=None):
         find_string1=pattern_line_w.search(line_to_write).group(1)
         find_string2=pattern_line_w.search(line_to_write).group(2)
         find_string3=pattern_line_w.search(line_to_write).group(3)
         if(find_string2.find(r'ST')!=-1):
          line_replaced=r'##define   R_'+list_vardetected+r'   '+find_string1+r'ST.'+find_string3
         else:
          line_replaced=r'##define   R_'+list_vardetected+r'   '+find_string1+r'st.'+find_string3

    elif line_to_write.count(r'[')==1:
        pattern_line_w=re.compile(r'^.*\W('+re.escape(component)+r'.*_)(pst->|st\.)(.*)\[.*\](\S*)\s',re.I)
        if(pattern_line_w.search(line_to_write)!=None):
            find_string1=pattern_line_w.search(line_to_write).group(1)
            find_string2=pattern_line_w.search(line_to_write).group(2)
            find_string3=pattern_line_w.search(line_to_write).group(3)
            find_string4=pattern_line_w.search(line_to_write).group(4)
            if(find_string2.find(r'ST')!=-1):
              line_replaced=r'##define   R_'+list_vardetected+r'(s_x_uw,e_x_uw)'+'   '+find_string1+r'ST.'+find_string3+r'[s_x_uw..e_x_uw]'+find_string4
            else:
              line_replaced=r'##define   R_'+list_vardetected+r'(s_x_uw,e_x_uw)'+'   '+find_string1+r'st.'+find_string3+r'[s_x_uw..e_x_uw]'+find_string4

    elif line_to_write.count(r'[')==2:
        pattern_line_w=re.compile(r'^.*\W('+re.escape(component)+r'.*_)(pst->|st\.)(\w+.*)\[.*\](.*)\[.*\](\S*)\s+',re.I)
        if(pattern_line_w.search(line_to_write)!=None):
            find_string1=pattern_line_w.search(line_to_write).group(1)
            find_string2=pattern_line_w.search(line_to_write).group(2)
            find_string3=pattern_line_w.search(line_to_write).group(3)
            find_string4=pattern_line_w.search(line_to_write).group(4)
            find_string5=pattern_line_w.search(line_to_write).group(5)
            if(find_string2.find(r'ST')!=-1):
             line_replaced=r'##define   R_'+list_vardetected+r'(s_x1_uw,e_x1_uw,s_x2_uw,e_x2_uw)'+'   '+find_string1+r'ST.[s_x1_uw..e_x1_uw].'+find_string3+r'[s_x2_uw..e_x2_uw]'+find_string4+find_string5
            else:
             line_replaced=r'##define   R_'+list_vardetected+r'(s_x1_uw,e_x1_uw,s_x2_uw,e_x2_uw)'+'   '+find_string1+r'st[s_x1_uw..e_x1_uw].'+find_string3+r'[s_x2_uw..e_x2_uw]'+find_string4+find_string5

    elif line_to_write.count(r'[')==3:
        pattern_line_w=re.compile(r'^.*\W('+re.escape(component)+r'.*_)(pst->|st\.)(\w+.*)\[.*\](.*)\[.*\](.*)\[.*\](\S*);',re.I)
        if(pattern_line_w.search(line_to_write)!=None):
            find_string1=pattern_line_w.search(line_to_write).group(1)
            find_string2=pattern_line_w.search(line_to_write).group(2)
            find_string3=pattern_line_w.search(line_to_write).group(3)
            find_string4=pattern_line_w.search(line_to_write).group(4)
            find_string5=pattern_line_w.search(line_to_write).group(5)
            find_string6=pattern_line_w.search(line_to_write).group(6)
            line_replaced=r'##define   R_'+list_vardetected+r'(s_x1_uw,e_x1_uw,s_x2_uw,e_x2_uw,s_x3_uw,e_x3_uw)'+'   '+find_string1+r'st.'+find_string3+r'[s_x1_uw..e_x1_uw].'+find_string4+r'[s_x2_uw..e_x2_uw].'+find_string5+r'[s_x3_uw..e_x3_uw]'+find_string6
            print(line_replaced)
            print(3)
    else:
        print('non_found')
    line_replaced=line_replaced.replace(r';',r'')
    line_replaced=re.sub(r'\=.*$','',line_replaced,)
    line_replaced1=''
    if(line_replaced.find(r'pst->')!=-1):
     line_replaced1=line_replaced.replace(r'pst->',r'st.')
     if(line_replaced1.endswith('\n')):
      file.write(line_replaced1)
     else:
      file.write(line_replaced1+'\n')
    else:
     if(line_replaced.endswith('\n')):
      file.write(line_replaced)
     else:
      file.write(line_replaced+'\n')
     #file.write(line_replaced)

# purpose is getting path of module under test, path of header file
def get_infor():
    path_input=os.getcwd()
    md1=''
    patterm_path_lib=re.compile(r'(\w.*sources\\comps\\(\w+))\\\w+',re.I)
    patterm_path_module=re.compile(r'(.*\\(\w+_*\w*))\\\w+\\\w+$',re.I)
    module_path=patterm_path_module.search(path_input).group(1)
    list_module=os.listdir(module_path)
    comp=patterm_path_lib.search(path_input).group(2)
    find_modulename =os.listdir(path_input)
    print(find_modulename)
    print(comp)
    for mdname in find_modulename:
        if (mdname.find(r'.ptu')!=-1)|(mdname.find(r'.stb')!=-1):
            module_name=mdname
    for module in list_module:
        md1=module.split(r'.')
        md2=module_name.split(r'.')
        if (md1[0]==md2[0]):
          if(module.endswith(r'.c')==1)|(module.endswith(r'.cpp')==1):
            module_full_path=os.path.join(module_path,module)
            print(module_full_path)
    path_lib = patterm_path_lib.search(path_input).group(1)
    module_script=module_name
    print(module_script)
    path_adapt= path_lib
    path_varmodule=module_full_path
    path_script= os.path.join(path_input,module_script)
    #get header file from source file
    list_file_path=[]
    list_file=[]
    file_objw =open(path_varmodule, "r")
    list_file_excep=['define.h', 'mat_pub.h','mfl_pub.h', 'norm.h']
    for line in file_objw:
       pattern_header=re.search(r'^\#.*\<(.*\.h)\>',line)
       if(pattern_header!=None):
         if(list_file_excep.count(pattern_header.group(1))!=1):
          list_file_path.append(pattern_header.group(1))
    print(list_file_path)
    file_objw.close()
    #go to include folder in sandbox
    path_head=re.search(r'^(.*)\\sources.*',path_input).group(1)
    #search DIAB path
    path_diab=''
    for re_path, pth_direct, file_pth in os.walk(os.path.join(path_head,r'project\sw\build')):
        if file_pth.count(r'filelist.txt')==1:
           path_diab=re_path

    path_include=os.path.join(path_diab,r'include')
    list_file_include=os.listdir(path_include)
    os.chdir(path_include)
    for file in list_file_path:
      if(list_file_include.count(file)==1):
        path_headerfile=os.path.join(path_include,file)
        with open(path_headerfile,'r') as fl:
            for line in fl:
              pattern_header=re.search(r'^\#.*\<.*(sources\/comps.*\.h)\>',line)
              if(pattern_header!=None):
               list_file_catch=pattern_header.group(1)
               list_file_catch=list_file_catch.replace(r'/','\\')
               list_file.append(os.path.join(path_head,list_file_catch))
    list_file_update=list_file
    list_file_path_update=[]
    for file in list_file_update:
        if (file.find(comp)==-1)|(file.find(md1[0])==-1):
          with open(file,'r') as fl1:
            for line in fl1:
              pattern_header=re.search(r'^\#.*\<(.*\.h)\>',line)
              if(pattern_header!=None):
               list_file_path_update.append(pattern_header.group(1))
    for file1 in list_file_path_update:
        path_headerfile1=os.path.join(path_include,file1)
        with open(path_headerfile1,'r') as fl2:
            for line in fl2:
              pattern_header1=re.search(r'^\#.*\<.*(sources\/comps.*\.h)\>',line)
              if(pattern_header1!=None):
               list_file_catch_update=pattern_header1.group(1)
               list_file_catch_update=list_file_catch_update.replace(r'/','\\')
               list_file.append(os.path.join(path_head,list_file_catch_update))
    list_file1=list_file
    list_file2=list_file
    #sort list
    for refer1 in list_file1:
        if list_file.count(refer1)>1:
            in_ince1=0
            for refer2 in list_file:
             if(refer1==refer2)&(list_file.count(refer1)>1):
              list_file.remove(refer2)
             in_ince1=in_ince1+1
   # print(list_file)
    return list_file,path_varmodule, comp,path_script,path_input,module_name


#get function which is needed to find variable then put to a list
def Get_functioname_fromfile_N(path_varmodule_f,comp_f ):
    list_group_vardetected=[]
    arrar_w=[]
    arrar_w1=[]
    file_objw =open(path_varmodule_f, "r")
    for line in file_objw:
       #print(line)
       line=re.sub(r'\(',' binh \n ',line)
       srt=line.splitlines()
       #print(line)
       for lm in srt:
        arrar_w.append(lm)
    for line in arrar_w:
    #   print(line)
    #   line=line.replace(r'(',r' binh ')
       pat_com=re.search(r'^\W*\/\*.*\*\/',line,re.I)
       if(pat_com==None):
        #pattern_var=re.compile(r'(('+re.escape(comp_f)+r'|vdb)[^\s]+)\([^\(]*\)',re.I)
        pattern_var=re.compile(r'\W((\w*'+re.escape(comp_f)+r'|vdb)[^\s]*)\sbinh\s',re.I)
        name_find=pattern_var.search(line)
          #print name_find
        if (name_find!=None):
          # if(name_find.group(1)!=r'FUS_SetVRefSyncTC_v'):
          #  print(name_find.group(2))
          list_group_vardetected.append(name_find.group(1))
    list_group_vardetected1=tuple(list_group_vardetected)
    for refer1 in list_group_vardetected1:
         if list_group_vardetected.count(refer1)>1:
            in_ince1=0
            for i,refer2 in enumerate(list_group_vardetected):
             if(refer1==refer2):
              list_group_vardetected.remove(list_group_vardetected[i])
              break
    print (list_group_vardetected)
    return list_group_vardetected,file_objw


#main process of a function list which input parameter are:

def process_rename(list_file,list_group_vardetected,file_objw,comp):
    array_line=[]
    index=[]
    list_newfunc=[]
    list_group_vardetected_updated=[]
    array_line_towrite=[]
    fv=0
    for file_path in list_file:
      array_line=[]
      file_objr = open(file_path, "r")
      for line in file_objr:
        array_line.append(line)
      file_objr.close()
      file_objr = open(file_path, "r")

      for line in file_objr:
        if(line.find(r'ats_xs_buscfg.h')!=-1):
            print(file_objr.name)

        for var_find in list_group_vardetected:

            #to ensure the function name needed to find is inline funtion

            if (re.search(re.escape(var_find)+r'\s*\(',line,re.I)!=None)&(line.find('INLINE')!=-1):
               if(line.find('VDB_X_GetMileageT20_UL')!=-1):
                 fv=1
               cnt1=0
               cnt2=0
               update=False
               for line_x in array_line:
                 cnt1=cnt1+1
                 # print(line_x)
                 if line==line_x:
                   update=True
                   ok_break=True
                 if update==True:
                   #print('updated')
                   if (line_x[0]!=r'}'):
                    if(ok_break==True)&(line_x.find(r'{')!=-1)&(line_x.find(r'}')!=-1):
                     detec_str=re.search(r'('+re.escape(comp)+r'|vdb)\S+(pst->|st\.)',line_x,re.I)
                     if (detec_str!=None):
                        list_group_vardetected_updated.append(var_find)
                        array_line_towrite.append(line_x)
                     update=False
                     ok_break=False
                     break

                    else:
                     #detec_str=re.search(r'('+re.escape(comp)+r'|vdb)\S+(pst->|st.)',line_x,re.I)
                     detec_str=re.search(r'('+re.escape(comp)+r'|vdb)\S+(pst->|st\.)',line_x,re.I)
                     if (detec_str!=None):
                       print(file_path)
                       print(line_x)
                       if fv==1:
                         print('ok')
                         fv=0
                         print(line_x)

                       if(cnt2==0):
                        list_group_vardetected_updated.append(var_find)
                        array_line_towrite.append(line_x)
                       else:

                        if(line_x.find(r';')!=-1)&(re.search(r'\W(\w*'+re.escape(comp)+r'\S+)[\.|\>](.*_\w+)\s*;',line_x,re.I)!=None):
                         line_x1=line_x
                         line_x1=re.sub(r'\=.*$',r' ;',line_x1,re.I)
                         line_x1=line_x1.replace(r')',r' ')
                         name_diff=re.search(r'\W(\w*'+re.escape(comp)+r'\S+)[\.|\>](.*_\w+)\s*;',line_x1,re.I).group(2)
                         list_group_vardetected_updated.append(var_find+r'_'+str(cnt2)+r'_'+name_diff)
                         array_line_towrite.append(line_x)
                        elif(re.search(r'\W(\w*'+re.escape(comp)+r'\S+)[\.|\>](.*_\w+)\s',line_x,re.I)!=None):

                         name_diff=re.search(r'\W(\w*'+re.escape(comp)+r'\S+)[\.|\>](.*_\w+)\s',line_x,re.I).group(2)
                         list_group_vardetected_updated.append(var_find+r'_'+str(cnt2)+r'_'+name_diff)
                         array_line_towrite.append(line_x)
                       cnt2=cnt2+1
                     #r'(('+re.escape(comp_f)+r'|vdb)[^\s]+)\([^\(]*\)'
                     new_mapfunc=re.search(r'\W((\w*'+re.escape(comp)+r'|vdb)[^\s]*)\s*\(',line_x,re.I)
                     if new_mapfunc!=None:
                       if (list_group_vardetected.count(new_mapfunc.group(1))==0):
                        list_newfunc.append(new_mapfunc.group(1))

                   else:
                     update=False
                     break
      file_objr.close()
      file_objw.close()
    print(list_group_vardetected_updated)
    #Update index and list_group_vardetected_updated in case there are more than 1 same value in list
    in_ince=0
    for gr_updated in list_group_vardetected_updated:
        gr_updated1=gr_updated.replace(r'(',r'')
        list_group_vardetected_updated[in_ince]=gr_updated1
        in_ince=in_ince+1
    return list_group_vardetected_updated,array_line_towrite,list_newfunc

#search for the pattern of varibale then rename as template. Finally, write to file
def write_array_to_file(path_script,path_input,list_group_vardetected_updated,array_line_towrite,comp,module_name):
    #write result to script file
    #read existing script file
    mdn=module_name.split(r'.')
    path_name1=path_script
    if(module_name.endswith(r'.ptu')):
     path_name2=path_input+'\\'+mdn[0]+r'_bk.ptu'
    else:
     path_name2=path_input+'\\'+mdn[0]+r'_bk.stb'
    print(path_name2)
    os.rename(path_name1,path_name2)
    path_script1=path_name2
    os.chmod(path_script1, stat.S_IWRITE )
    f_script=open(path_script1,'r')
    os.chmod(path_script1, stat.S_IWRITE )
    f_script_out=open(path_name1,'w')
    #line_read=f_script.readlines()
    cnt = 0
    indentify=0
    index_add=0
    for i, line_read_child in enumerate(f_script):
      #print(line_read_child)
      cnt=cnt+ 1
      if (line_read_child.find('-- Declarations of the global variables of the tested file')!=-1):
         index_add= cnt
         idx=0
         indentify=0
      elif (line_read_child.find('// Additional files:')!=-1):
         index_add= cnt
         idx=0
         indentify=1
      if (i==index_add)&(i!=0):
        for lw in array_line_towrite:
          if(idx>len(list_group_vardetected_updated)-1):
              break
          if lw==array_line_towrite[0]:
           if(indentify==0):
            f_script_out.write('-------------------------------Start defining variable-------------------------------\n')
           elif(indentify==1):
            f_script_out.write('///////////////////////////////Start defining variable///////////////////////////////\n')
          write_vartofile(f_script_out,lw,list_group_vardetected_updated[idx],comp)
          idx=idx+1
      else:
         f_script_out.write(line_read_child)
    #print(list_group_vardetected_updated)
    #print(array_line_towrite)
    f_script.close()
    f_script_out.close()
    os.remove(path_script1)
    #print (cnt)
def core_rename():
   list_file,path_varmodule,comp1,path_script,path_input,module_name = get_infor()
   list_group_vardetected,file_objw = Get_functioname_fromfile_N(path_varmodule,comp1)
   list_group_vardetected_updated,array_line_towrite,list_newfunc=process_rename(list_file,list_group_vardetected,file_objw,comp1)

   while(True):
    if(list_newfunc==[]):
      #Finally update the list before writing to file
      list_group_vardetected_updated2=tuple(list_group_vardetected_updated)
      list_group_vardetected_updated1=tuple(list_group_vardetected_updated)
      array_line_towrite_update=[]
      Q_1=0
      for refer1 in list_group_vardetected_updated1:
         if(refer1==r'VDB_X_GetPlausTurnLeft'):
            Q_1=1
         if list_group_vardetected_updated.count(refer1)>1:
            in_ince1=0
            for i,refer2 in enumerate(list_group_vardetected_updated):
             if(refer1==refer2):
              if(Q_1==1):
               print('ok')
               Q_1=0
              list_group_vardetected_updated.remove(list_group_vardetected_updated[i])
              array_line_towrite.remove(array_line_towrite[i])
              break
     #debug
      write_array_to_file(path_script,path_input,list_group_vardetected_updated,array_line_towrite,comp1,module_name)
      break
    else:
       list_group_vardetected = list_newfunc
       list_group_vardetected_updated_add,array_line_towrite_add,list_newfunc=process_rename(list_file,list_group_vardetected,file_objw,comp1)

       for go_line in list_group_vardetected_updated_add:
        list_group_vardetected_updated.append(go_line)
       for go_arr in array_line_towrite_add:
        array_line_towrite.append(go_arr)
if __name__ == '__main__':
    core_rename()
    pass

