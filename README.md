# Single-base Mutation, Dan Graur 2008
# You can find this paper in http://ow.ly/g0wC301CALf
# Script developed by Divya Selvaraju
#! /usr/bin/python

codon={}
with open("codontable_wo","r") as text:  
	for line in text:
		key, value=line.split()
		codon[key]=value
	n={1,2,3}
	count_tsyn=0
	count_tnsyn=0
	for j in n:
		m=1
		count_syn=0
		count_nsyn=0
		count_non=0
		count_mis=0
		for i in codon.keys():
			l=[]
			l.extend(i[0])
			l.extend(i[1])
			l.extend(i[2])
			nt=['A','T','G','C']
			a=''.join(l)
			l[j-m]=nt[0]
			b=''.join(l)
			WC=codon.get(b)
			WOC=codon.get(a)
			if a!=b:
				if WC==WOC:
					#print "Synonymous mutation : %s -> %s" % (a,b)
					count_syn+=1
				else:	
					#print "Non-synonymous mutation : %s -> %s" % (a,b)
					count_nsyn+=1
					if (b=="TGA")|(b=="TAA")|(b=="TAG"):
						#print "Non-sense mutation : %s -> %s" % (a,b)
						count_non+=1
					else:
						#print "Missense mutation : %s -> %s" % (a,b)
						count_mis+=1
			
                	l[j-m]=nt[1]
                	b=''.join(l)
                	#print b
                	WC=codon.get(b)
                	WOC=codon.get(a)
			if a!=b:
                		if WC==WOC:
                                	#print "Synonymous mutation : %s -> %s" % (a,b)
                                	count_syn+=1
               			else:
                        		#print "Non-synonymous mutation : %s -> %s" % (a,b)
                        		count_nsyn+=1
					if (b=="TGA")|(b=="TAA")|(b=="TAG"):
						#print "Non-sense mutation : %s -> %s" % (a,b)
						count_non+=1
					else:
						#print "Missense mutation : %s -> %s" % (a,b)
						count_mis+=1
			l[j-m]=nt[2]
                	b=''.join(l)
                	WC=codon.get(b)
                	WOC=codon.get(a)
			if a!=b:
          			if WC==WOC:
                                	#print "Synonymous mutation : %s -> %s" % (a,b)
                                	count_syn+=1
                		else:
                        		#print "Non-synonymous mutation : %s -> %s" % (a,b)
                        		count_nsyn+=1
					if (b=="TGA")|(b=="TAA")|(b=="TAG"):
						#print "Non-sense mutation : %s -> %s" % (a,b)
						count_non+=1
					else:
						#print "Missense mutation : %s -> %s" % (a,b)
						count_mis+=1

			l[j-m]=nt[3]
                	b=''.join(l)
                	#print b
                	WC=codon.get(b)
                	WOC=codon.get(a)
			if a!=b:
                		if WC==WOC:
                                	#print "Synonymous mutation : %s -> %s" % (a,b)
                                	count_syn+=1
                		else:
                        		#print "Non-synonymous mutation : %s -> %s" % (a,b)
                        		count_nsyn+=1
					if (b=="TGA")|(b=="TAA")|(b=="TAG"):
						#print "Non-sense mutation : %s -> %s" % (a,b)
						count_non+=1
					else:
						#print "Missense mutation : %s -> %s" % (a,b)
						count_mis+=1
		count_tsyn+=count_syn
		count_tnsyn+=count_nsyn
		tot=count_syn+count_nsyn
		syn_per=round(float(count_syn)/float(tot)*100.0)
		nsyn_per=round(float(count_nsyn)/float(tot)*100.0)
		non_per=round(float(count_non)/float(tot)*100.0)
		mis_per=round(float(count_mis)/float(tot)*100.0)

		print "Total mutations in pos=%s         : %s\n" % (j,tot)
		print "Synonymous mutations in pos=%s    : %s\t%s %%" % (j,count_syn,syn_per)
		print "Non-Synonymous mutations in pos=%s: %s\t%s %%" % (j,count_nsyn,nsyn_per)
		print "Missense mutations in pos=%s      : %s\t%s %%" % (j,count_mis,mis_per)
		print "Non-sense mutations in pos=%s     : %s\t%s %%\n" % (j,count_non,non_per)
	t=count_tsyn+count_tnsyn
	s=round(float(count_tsyn)/float(t)*100)
	ns=round(float(count_tnsyn)/float(t)*100)		
	print "Total mutations                  : %s\n" % t
	print "Total synonymous mutations       : %s\t%s %%" % (count_tsyn,s)
	print "Total non-synonymous mutations   : %s\t%s %%" % (count_tnsyn,ns)
