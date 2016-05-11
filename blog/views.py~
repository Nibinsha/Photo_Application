from django.shortcuts import render
from django.shortcuts import render_to_response
from django.template import RequestContext
from django.http import HttpResponseRedirect
from django.core.urlresolvers import reverse

from .models import Document
from .forms import DocumentForm
from PIL import Image
import glob, os


def index(request):
    return render(request, 'blog/index.html',{})

def list(request):
    # Handle file upload
    if request.method == 'POST':
        form = DocumentForm(request.POST, request.FILES)
        if form.is_valid():
            newdoc = Document(docfile = request.FILES['docfile'])
            newdoc.save()

            # Redirect to the document list after POST
            return HttpResponseRedirect(reverse('blog.views.photo'))
    else:
        form = DocumentForm() # A empty, unbound form

    # Load documents for the list page
    

    # Render list page with the documents and the form
    return render_to_response('blog/list.html',{ 'form': form},context_instance=RequestContext(request))

def photo(request):
    documents = Document.objects.all()
    return render_to_response('blog/photo.html',{'documents': documents})
    
    

# Create your views here.
