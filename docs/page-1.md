---
hidden: true
---
New Test


# Page 1

hello everyone present here uh uh today
we are going to have another round of in Workshop which will include our in wallet module uh so it's pleasure to
have you all uh for today's Workshop we have our whole in team present here so
I'm Sanji Singh product owner for in and I'm thrilled uh to be leading this
session along with lot of key members present from our team and uh today we
have joined by our principal architect vishwanath our experts uh technical
leads of different modules of in we have swti goyel we have Vijay Kumar we have
shrat and hites Jen we have our product manager uh project manager of fi prti
also present here so she'll also be taking us through a lot of things today I'm also excited to share we have a
senior leadership team with us including Ramesh Naran and our C which is who is
our C and Sashi Kumar are our head of engineering as well as the whole mosa
product team through whatever we have seen in the previous discussions and sessions we have explored the core
feature of in which is in certify the issuance module and today we are diving
deep into the Practical side with Hands-On solution building for our ing wallet which is a holders application
how users um can use this NG wallet and how it is practically built which will help uh uh attendees present here and
the participants of the webinar today's Workshop will cover uh different integration capabilities of in wallet
we'll start by demonstrating how to create an oidc client on board mimoto
configure a new issuer and build in wallet from scratch and how you can
download uh the different credentials so we have picked up one use case for today
which is Farmers credential so we are going to talk about how we are going to to use Farmers credentials what we
showcased in the last uh demo and the workshop that how the farmer credentials
are issued and how we'll be able to download it uh using our in wallet holders application so there are lot of
things technically that my team will be taking you through finally we are going to guide you through these components
how they work together how they're interoperable and inclusive in nature we also have a dedicated Q&A session at the
end of the uh webinar but to address any question between the webinar session please feel free to drop
your questions we have our team present here we'll be answering those questions in the Q&A Dropbox uh additionally
please note this session has been recorded so later on this will be provided as a resource on the webinar
website and the in documentation which will be providing the link to you shortly on the chat box uh STI and prti
over to you you can take forward the session thank you everyone thanks
Sian so hi STI how do you want to take the session what are the different steps
that you would be taking today Yeah so basically as uh Sai mentioned right NG
wallet right so in wallet we have two component known as NG mobile and NG web
right so these are the two instances of wallet now how they get the uh VC
downloaded so both are depend and only one service backend service which is known as mimoto so we will first cover
this mimoto part right then then we'll see how through mimoto we can download the
VC okay so yeah so let's go through the mimoto first what is mimoto and how it is interacting with wallets so it is as
I mentioned it is simple backend service so obviously it's written in a spring board backend service once backend
service is expose it expose through some port number right so the port number we
are using for mimoto is here 18899 now you are going to build uh this
mimoto locally right so that you can download and see the credential locally but mobile cannot access the Local Host
right mobile will be a physical device then how can you access mobile uh this Moto through mobile so we are using free
version of NG NG that helps us to do a port forwarding so we can expose our
mimoto Port through njo and access from the mobile right that's the one thing we are doing on the wallet side that we
will see when we go through the demo second in the in web so in web is also running on your Local Host is some web
interface so it is running on the 3,000 Port now uh this is what we are going to
cover today but we are not going to use EET locally we are going to rely the E
Signet deployed on our collab sandbox environment right so this NG web has to interact with the uh e signate outside
our Local Host environment so we get that course issue of interacting from
signal from the collab environment and requesting back to the in web to avoid that course ER what we are doing is we
have WR a web proxy so basically web can interact with the proxy and proxy can directly go to
the mot to and download the VC okay so the reason why we are doing this is to
ease our develop devopment local development okay got it sir thank you or
if you in any CL environment you don't need this NG and web proxy things can be accessed through
service recovery within that cloud clusters right yeah this only for the local development now let's jump to the
mimoto how easily it is just to configure one issue or download the VC in this very few steps so what I've done
is okay so I have used the latest version
of mimoto I have p on this rep from the remote app stream I will configure a issuer here okay so let's go to the Cod
base so this is the mimoto as I mentioned we don't we are not using EET
locally right but we have to authenticate through EET because EET is our authentication server right to do
this what we need we need some onboarding of mimoto to interact with the EET right so the EET can
authenticate okay request is coming from a valid server so for this we need to create a client ID okay that is well
documented in our documentation as well if you go inside NG mobile customization section credential providers we have
mentioned the steps like how can you use uh onboard mot as IDC clients so one is
you can use our mock data and use our sandbox collab environment to authenticate and download the VC other
one is you can create your own and get the things done everything in your local setup okay so for the time being I'm
going to use the e sign uh from the collab environment I have already gone through all these steps
created a client ID against ignet on collab environment and I have got the p12 file also configured with me so I'll
show you what is that so let's come to this class okay got so
basically what you're saying is it is all documented and for people the steps are given even the p12 file is also
there in the documentation and they can use it from there yeah
thanks now let's create an issu okay so we have a file called mimoto ISS configuration this is basically a
trusted list of issu for the wallet here we can configure any number of issuers what we want to support in the our any
wallet so right now as s mentioned we are going to take a use case of farmer so this is the credential id issuer id
which is has to be unique per issuer so we have named it as a farmer this is the display property which is being shown on
the UI like these are the list of isual supported okay you see this title on the UI like the for credentials and all
these things protocol you can ignore this is just to differentiate different type of protocol uh in wallet can
support right now we are supporting oppon for VC but this is the extensible code for future if we can extend more that we can add different type of
protocol support client ID as I explained already this is what we onboarded on the NG e
Signet mock on the collab environment so that's the Cent ID we have created and when we are creating a keyp generation
so that time we have created a client alas that's the same thing we have mentioned here coming to line number 20 redir Ur
So what happens you are using a wallet you say okay download a VC selecting an
issuer that will redirect user to the EET page that's a web view gets open within application right now once you
authenticate you needs to know where to go back right after authentication so this is the r Ur for that and that is
the red Ur we have configured in the NG Mobile Wallet now now coming to the Token
endpoint and author audience so token endpoint is nothing but basically um
when you authenticate through a signal you need to give few Secrets right what is your uh like uh you create a jot and
proof to get the exess token but all those secrets and private Keys you cannot keep in the mobile right so it
has to route through some server so we have used mimoto as a proxy in between
so what happens wallet interacts with the mimoto mimoto construct the request
to get the token from a Signet and return it back okay so that's why you see this token endpoint line number 21
is the endpoint which belongs to the mimoto and you could see I have used the
ngok URL here because this to on endpoint will be accessed from the mobile right it can't be Local Host
proxy toer endpoint is the actual endpoint which is served by E Signet which is authentication server as of
today authen audience e Signet needs to know for which audience I'm going to issue that that is also we have
mentioned here welln endpoint so we already covered this in
the last session of certify this is the basically this is based on the open for VC specification it gives you each and
every information about credentials supported by the issuer how many credential are supported what to display
on the UI for the credential type right what will be the claim sent in the credentials you can even display the
properties like per language for Loc Lo so let's say I'm these are the credentials claims we are going to have
in this credential right so you can configure different different locals here as well you want you can even
configure what should be the background of your card which you see on the mobile what should be the text you want to show
so all these things can be easily configured through well known all right
second is 25 line number is embedded VC so this is for the in web not for the
mobile this is basically to configure the entire VC into a QR code that can be
scanned through a NG verify component and you can verify okay and last is just
a simple feature mentioned here enabled you can enable disable based on your requirement so it's a configuration so
you don't need to rebundle mimoto or your wallet to support or add or remove
any support of issuers so these are all about the mimoto issuer configuration file got it so basically after
onboarding I need to set it up with mimoto here saying these are the issuers
and we can configure them here okay so this what is the authentication what is the issuance and what is the wellknown
these are some of the key things that we would have to do it here okay yeah and
uh one thing we have already covered in the last session but I will again just touch that point this is the Au server mentioned here right so we are using e
signal deployed on the collab environment if you want to use any other authentic authentication server auth
server we have it can be easily replaced through the welln only okay yeah that's the one thing second uh as I mentioned
like when we generate a key uh client ID that time we also need to create a p12 file that's a secret all the key store
and the uh secret contains in this file so once you generate this file it gets loog with some key right so mimoto will
be Consulting a token request so it needs to read this file right so that file has to be unlock so for
this we have set a password for this file and that is for us in this
session is M 123 okay so that uh mimoto will use to unlock this password read
the data and cons the Cen request okay so these are the only things we need to
onboard any is into Moto one oidc client creation then you
will get the p12 file and then configure the ISS that's it okay now let's start we have
configured the mimoto issuer let's see whether it's working or not so I'm going to use the doer compost setup locally so
for this all this configuration which we mentioned here right this config folder these are not bundled with the
application these are we are serving from the spring Cloud okay for this session we have used the engine to serve
this configuration for us because we are not inter with the cloud secondly this search folder if you see for this
session we have built in the doal compos for the local development but ideally in your Cloud environment it's mounted on
the mimoto port okay so yeah so if you see it's serving all the configuration mentioned in the
config folder and this is simply uh I have built this mimoto locally I'll show you how to build that also and some
environment variables which configuration we are going to load and then volume hounting of this configuration from engin to our mimoto
instance right yeah so let's go to
mimoto so one thing is mimoto is on Java 21 okay so we can just confirm our Java
home it's Java 21 so we can easily build to make if you want to make any changes
let's say you want to debug something right you need to bundle the jar create the blocker image again we can easily
use may1 command this I have added just to uh fasten the process SK skip the test while bunding the jar this will
create a jar in the Target folder that you can see here
this mimoto Java 21 snap there right this gets are created you can directly
use the docker command Docker build minus t I think
people who knows doer they know what this means this is the service name this is the tag name dot is the where the doer file exist so this will build your
Docker image okay and then whatever name or tag you give to Docker image you can directly use in the docker compos
file okay this is based on the customization you want to do in the toer and use the Doer image locally built if
you want to use any release version of mimoto so when we do a release we mention what is the doer release images
you can directely use this mimoto any release image okay so for now uh I'm just going
to use locally built images so I have this mimoto local
build yeah so that's the one thing let's start the Mot
so it is started the engine engine is started and you can see the
configuration for mot is also getting started okay by the time mot is starting you can
you could see in the it was using the old file we also have to start the proxy for
web right that will come later so mimoto is started you can see through validation of is config is also
completed for local setup you can ignore this web sub error these error comes for
one of our very old use cases that web doesn't uh applicable for the local setup so you can ignore this web sub
error when you see mimoto running in local I see that my Moto is uh up but
how do I know that it is working yeah so I as I mentioned look we can see confirm
in the doer compos also we are running on 1899 C right mhm 18 99 SL list of
issuers so whatever issue I configured into the code you could see it here as well directly right all these things
will be same we could see in the Json file yeah and we can config confirm this
through NZ also so that like it will be served by mobile also so this is the NZ URL I'll just put it
there it is serving the same data okay nice basically what we did is we
onboarded the client we added uh issuer and then running up the mimoto we are
able to see that the issuer is we are able to see the listed issuer okay
yeah cool what is the next so our mimoto back end is ready now we have to focus
on the wallet how can we download this issue which we configured right now so I will go to the NG
wallet okay NG wallet is a retive application so react native support Java
171 okay so we have to check which version of java we have so in this terminal version uh instance I have
configured the Java 17 okay for this uh it's a reactnative application so basically you can use
npmi to install all the dependencies that I have already done and then there's a command already
mentioned in the documentation about build and deployment build and
deploy it's getting loaded so for Android and iOS all the steps are mentioned here in detail okay
so that's the simple thing for build and deployment now let's focus on customizing the
theme or any changes in the UI we want to do first we will start with the theme
that is like makes interesting uh things on the mobile side like anyone can
use uh any themes based on their requirement or like based on the wallet being used in which which context so
basically what we have is there is a style utility file we have return this
style utility file is nothing but it says this is the theme attribute which will be referred across the
application right so right now everyone know like IND W supports to purple and orange so that's why it's conditional
check but if you want to ignore this you can just ignore this environment variable and directly write default
theme as well so that wallet will support only one thing right but how to configure this
thing yeah so it's simply if you see from where we are importing it it is
from the themes folder the theme folder you can see on the left side right is simply one constant only what you have
to do create a new file let's say new
theme what timeing TS okay inside this you have to export this file so that can
be imported into components it's
simple new theme
okay simple object now you can write all the Styles
and everything here exported so whenever I will refer this new theme it will be referred like theme do something theme
do color theme do style right so that's the only thing you need to have it to
support any new theme and if you see the existing theme default theme and all we have so many sty based on the
functionality or the pages or the UI component we have in the applications so we are supporting these themes some
styling and the all fixed colors we just need to change value of these attributes
based on our requirement okay and for the standard one we have mentioned the documentation as well uh like you want
to change the application logo you want to change the theme already mentioned here you want to change the home screen logo you want to change the header logo
everything is mentioned here what can you change okay what we have to do is create a new
file uh create a constant object and then we can have the default
theme and uh then follow our documentation to update the specific areas that we need to change yes yes so
for this demo I have just created this green theme which is new it's the same
copy pasted form existing theme file and replacing few colors and change that's
it okay so I'm going to use green theme now that's the one thing now second
thing is the local so we are supporting six locals right now mentioned here in the documents these are the simple four
steps you want to do to support any other languages add one Json
file and use that Json file into the I8 TS and add in the these two compon uh
constant resources the support languages and how to use that is simply mentioned here also this is the one hook
exposed by this uh like a react and I like use translation and whenever you use this you have to refer that way I
can just refer to one of the local
file so if you see I want to use this backup in store title right so it will be
like t s small T backup dot title
so you write this way it will read this okay so this will
get picked up in the reference so it's that simple so you can just add simply one more loc here and get the things
done for the different locals got it and all of this is also there in our
documentation yes everything okay
yeah there's one more thing I just want to say in the loc customization which which is not very frequently used it
depends on the use cases workflow customizations this workflow is nothing but uh basically like we are using
reactnative right re native drives how you want to navigate a user as well
through the screens plus how to maintain that navigation in the code right so this we have used a retive access State
these are the main states we have in the applications you can use this NG wallet
the way it is today you don't need to make any change the customization workflow customization but if you have some requirement you
want to add some or change some flow in between of the user experience as well
then you might need to add the new state Machine new workflow and everything has
to be there how to do that it can be easily read you can easily go through the ex State setup and follow the steps
mentioned in this documents okay yeah
okay so now we have the mobile customization done we are also set up
the localization basically I can add new language support also and we have also
seen how to add additional workflows yes okay what next we want to do now now
let's build this and trite on the mobile and see whether it's working or not are we able download or do we see some error
run time let's see that okay so to share my screen I am using viser
uh just to so that I can show my connected device
here fine so I have already done the npm install so all my dependency are already install
because that takes time so I skip that part as part of the workshop just to save some time this is the command
already mentioned in the document as well how to run and build for Android I'll run this command it will create an
APK
by the time it works maybe we can focus on
the mobile uh browser
okay yes
that's we want to look at the yeah because it APK Tak sometimes 2 three
minutes now so let's utilize that time sure
yeah so as I mentioned in that start we are going to use a web proxy
to aoid the course error you can see we have this web proxy here and then we
have to just go to the NG web proxy you don't need to make any changes you just need to build a Docker image if you want
to use through Docker or thatly you can use npm commands right so you can just need to use
uh toer build in the web proxy and use it okay
so I have already built it but I can again rebuild that's not a issue let it build and then we can start this through
doer as well so in the mimoto I'll just use this so I'll
explain all the compon uh variables also here this is the NGB proxy this which I buil this image locally I'm using 310
port to export that uh port so that can be accessed by mobile sorry web and this
is the mimoto as both are running in the same network they can do the service Discovery directly through this port and
the service name that's it okay that's the only thing you need
to start this so basically we are giving the port
and the needed details for uh yeah the web to run
yes now let's uh the uh since mimoto is
common uh mobile and web so I don't have to onboard the issuer again the same issue
can be used for both web and wallet right I mean mobile and web yes okay so
now let's start this web Pro as I added now only in the doer compose so I will
go to doer
compose we start the proxy how can I verify this just hitting this
URL it is accessible now I'll head the issuer so if you see mimoto is already
appending V1 mimoto right so I don't I don't need to append this into the proxy server proxy I'm just saying give me the
isser it is redirecting request to the remoto P okay so my web web proxy is up
and running now let's jump to the
building NG web okay NG web is basically faster than building the
APK so if you see APK is still happening so let's do that what time so
I will go to inside NG web folder it's simple react application again okay so let's go to this
cool now similarly what we see in the NG wallet right mobile site how can you
customize this how can you change the theme how can you change the local same thing we can achieve in the NG web as
well okay I'll again go through the documentation only which to refer later
yeah PR no uh I just wanted to say we have a documentation from where I can refer it right yes everything is there
there if you see UI customization we have mentioned how can you change the new theme okay and as well as how can
you change the local okay yeah everything is there so I'll just follow
the same steps and then you can do this OB you see we have this index CS files which are serving the theme I can just
add one more theme here and that will serve it okay fine so let's yeah let's
go to this file so we have this index CSS as mentioned so we have also added
the same green theme here as well it's nothing but you have to just keep referencing of all these properties and
change the value as per your theme nothing else nothing fancy okay that simple for the loc it's
same thing add one more loc and add the support in the I that's it but now how
do you know I need to know this refer to this theme right so what we have is we
have this EnV configurations
it is outside actually let me just open project from the
outside yeah so we have this NG configurations okay here if you don't
pass any theme it fall back to the default theme default theme is nothing but this
root okay if you want to change any theme you can just VI and bundle it here
and if you see we have other properties as well en which is a default language
the title I want to give to my wallet and this is nothing but the mimoto host for the NG web as I explain
the diagram mimoto is not the mimoto host right for NGB proxy is the mimoto host proxy is connecting to the mimoto
so that's why we are mention the proxy URL here right cool so this way we can change the
loc as well as the theme yeah py you have anything oh no I
good cool so let's go to there so it's again as an reactnative application I
will use NPI to Ure the dependencies let's see my APK is ready sometimes APK get in the installation side if you see
it's taking five minutes but it has been built that's why it is saying the command like installing APK so what we
can do is we can just Lo it failed itself sometimes we can just avoid this
and stop the and do manually okay so how you can do it so let's see where the application uh this APK get installed so
this is the path Android build outputs debug sorry resident and debug okay so
if you see these are the different different versions gets created I can maybe try to show the timing as
so Android app build outputs APK resident T debug build so all the builds
are here time is today modified is 5:31 only
right all the apks so we use the universal APK which gets compatible to install different versions of devices so
I'll just use the ADB I will check whether my device is connected or not it is connected I'll switch the device also
and I will use ADP install the command it is nothing but the path of the APK now it will install
the
application okay so our APK was U we were building the APK now it is built
using ADP we want to run it and see how it is working yeah so it is installed
successfully you can see the message here I can see the NG also installed here right and as we all know we have
changed the theme to Green so that's why you will see all the green color here okay so let's
navigate through this I'll just uh skip forgot one point I'll just cover that
also quickly I've covered the customization part everything right but I miss telling you how in Mobile is
interacting with Moto right so here also we have this EnV file right this is the
mimoto host so I've have configured my NGO server URL so that mobile can interact with it these are the default
thing like default application theme default language everything is explained here okay and what is this Google client
ID so uh NG supports backup and restore feature right that backup and restore
feature requires uh like a creating a client on the Google Play Cloud so that we have created and it's a secret so
that's why it's not exposed in the document on the code as well but how to create a client on the Google that is
already documented in our documentation so you can go here in the build and deployment step
itself go to n mobile go to build and deploy there's a
section uh setting a Google AP service and client ID for backup and restore we can follow these steps that will give us
the client ID that Cent ID we can use and configure here to use the backup and restore feature for the local development as well
okay yeah so yeah that's the thing I miss to cover in the wallet side
earlier cool so let's back to the application so these are the setups
screens I'll just skip it moves to the unlock method I'll do later I'll just
set up the passcode so don't think about this keyboard is also game because of the theme by mistake I change the
keyboard theme for some testing purpose so that's why the keyboard is coming green but it's not because of our theme okay
okay and the green theme is because we configured the default as green yes yes
now if you see these are the settings right these are the registry the same thing this is the mimoto host you can
see the Nero same URL here okay now yeah how to download the
credential here right so this is the plus icon mention here tap on the plus to download the
card so this is the farmer credential if you want to see whether it's the same thing which we could see on the API and
all so if you see title is down farmer credentials download credential with your farmer ID that is what you can see
it might be little distorted UI because of viser is showing that but that's the
same thing then farmer credentials that is served by the wellknown endpoint so
if you click on this wellknown it is giving you the display property which tells what is what type of credential
type name I have to display on the UI what is the logo logo is also mentioned here basically the issuer is telling how
the isser has to be um named and what is the logo yeah farmer
credentials I'll use credential which I have configured
yeah so it is authenticating now downloading a
credential so it will download the credential and display based on this
order defined in here in the detail space you will see the same order and this background you see some background
image that is also defined here in the um well known background image if you can see in the background of the
browser back is telling us how it has to be
displayed what is the background image and what is the order in which the claims have to be
displayed so yeah so basically this is what you see on the farmer side okay now
it also has the QR code right this QR code can be verified so we can use
either a upload feature or the scan feature let me just try out the scan
feature so for this we can directly use our NG verify module deployed on the collab environment so this is the host
of the collab where all the applications are listed in G verify you can go here
and let's try the scan feature I'll just disconnect the phone for time being because the wire creates a problem
sometimes I'll scan this QR code see it's so simple you scan the QR code that
is verified and now if you want to see the upload that I will explain through NG
web okay so this is what we could see in the NG mobile prey okay thanks then U basically we
have been able to down build the APK run it and able to download one VC and scan
it through the NG verify yeah the similar things on NG web yes so
let's start NG web so starting 3,000 Port this is the
homepage of the NG web if you could see we have changed the theme to Green so you could see this Bon is a green some
icons which are SVG image also in the green on the top right this language icon and all so let's click on this it's
the same Agro vas issuer here it the same credential type supported here
right it will again use the same thing we will download the same credential
here everything same it's just like two interface we have given one is mobile
one is mobile web and mimoto is same for both of them
that is the same list of issuer is shown yes so downloading in progress we have
successfully downloaded the VC you can see this VC go downloaded okay this is the QR Cod which is embedded to verify
now let's verify this I'll use the upload feature here now this is the one I just created if
you see today 543 time it's verified right so this is end to end how
can you configure an issuer in mimoto and use it on the both the platforms of NJ wallet web and
mobile thanks for this good so I see that from NG web we have been able to
configure run it locally download the VC and upload the same feature upload the
same verifiable credential and verify it using the in verify yes
yeah yeah so that's all about how to use NG wallet locally how to build it how to
customize it right how to add loc support same Lo change logos use
existing features as well so one thing I'll just point out at the end like what
we have done to simplify the process for people to try out an integrators
basically uh we have onboarded one client ID okay that people can use and
configure into their own um system so let's say they have some is provider
right but they want to use our authorization server signant so they can directly just use this exposed
one and it's simple like just uh I mention this in the Von and it will re
user to the collab and they will authenticate and then get the data from their own data providers
that how to do that that was already covered in the N certifi session how can use different different data providers and use the plugin to write
that then we good for we can can open
for yeah I will stop sharing so we can
discuss the questions either on the chat or maybe if somebody has question
we are open for uh Q&A so if there are any questions feel free either to put it
on the Q&A session or raise the hand if you want to discuss
further did they ask questions coming up so many so let's take one by
[Music] one how is the credential validation happening
okay so Kiran has asked this question so basically for credential verification
and validation we have written a library so we have not covered this in this session we were thinking to cover a
separate session for all the libraries we are writing so this is the VC verifier Library we
have written it is very validated and verifying the VC as well so I think K if
I understood your question correctly the validation and verification you mean uh like is the proof which is being
like passed as part of VC response is valid or not all the credentials data we get in the credential response right the
context the credential subject and the proof section all these are valid or not right so whether credential is expired
or not so all these things is man uh done through this verifier Library d by and integrated into Mobile and by
both okay next is is VC following WTC data
model yes we are following WTC data model 1.0 and uh we are working towards
supporting 2.0 as well
now can we demonstrate the IDC client on boarding and p12 flying conation okay so
I think let's take it little towards the end so that we can answer the question but that was already
covered during previous session but we will just walk through quickly also here okay snat we'll do
it so Kiran has one more question also when the farmer ID was entered to download the credential how is
authentication with the end user happening uh I'm not getting that part how is authentication with end user
happening STI I think the question is on the eant kbi or maybe that's the
question maybe I mean which did you get that question like how the authentication with the end are happening are we saying how are we
knowing what are the foral ID we are entering that is related to the VC credential maybe if can we unmute K and
maybe ask this if possible Vish I was asking a question
right like he mentioned about he she sorry I don't know sorry for that yeah how is authentication with the end user
happening okay okay so this particular use case uh we use a authentication
mechanism called kbi which is knowledge based identification so this uh is
supposed to be used in a very uh low Assurance use cases where we don't want to be 100% sure that user is indeed
involved in this but this is more of a retrofitting um uh option that is
available for authentication that can be used for downloading some low Assurance use cases
credentials um but if you're asking me uh Is it wise to use it for kind of
national ID kind of a credential it's not a wise thing to use but this is just an option that is available in our
system today uh we also have other authentication mechanisms as part of EET
and NG certify uh which are all um OTP and biometric based as well uh so
today's use case demonstration was done using the um knowledge based identification where you saw uh the
farmer ID and some some details of the farmer is given to down download the
credential um uh STI is it possible for us to show the other uh mechanisms authentication
mechanisms somewhere okay so I was just showing this also when you create a client ID that time you can configure
what kind of authentication you want to support right so visha you are asking if do we have anything let me just check on
the collab environment once okay yeah somewhere in the E Signet if we can just show them the options that is
available so we can tell them based on the use case um and the assurance that
is required uh the authentication Factor can be decided by the issuer H okay
let's go there if you see this is the EET code so you can use ass signning with EET right so here you will see all
this supported authentication method OTP that what VMA mentioned Biometrics and the Lo with mobile okay so this gets
created when you generate a client ID right that time you have to specify the ACR that drives this information so if
you configure the knowledge also you will get the knowledge base authentication as well
here that's what you want to do so right which
one cool so this is done what what is the next question we
have how can one configure data model or onology for New verif Vertical such as
digital travel credentials based on the io standard not VC uh which do you want to take that
question you on mute I think for speaking you're on mute sorry how can one configure data model onology for New
Vertical such as digital travel credential based on the I Ico standards not VC
okay uh yeah uh S I can take this um currently uh what we are supporting as a
credential format or credential profile you can call it is uh only the
verifiable credential of w3c data model 1.1 uh we are also working on supporting
data model 1.2 uh sorry 2.0 and um there's also some work going uh to
support uh M do mdl so these are the various things that we have prioritized so to come to your question the iov VC
uh would be a customization uh in the code but it follows the same uh protocol
uh most of the code will be same but some areas that needs to be customized to follow follow the iov standard and uh
if the model fits into the open ID for VCI flow then the respective customizations will be very simple for
us to uh include so but it's it's not supported
out of the box it's going to be a customization uh in the models um modules like NG certify and valet so for
all these places it doesn't understand the new credential type I believe IO standards uh will be a new travel
credential type uh which needs to be um added as an support into all these three
modules for the end to end uh
functionality so that is done okay so let's move to the question by day is it
required to use NG wallet with NG certify and verify or they can stand on their own okay so yeah so every module
is independent you can only use NG certify if you're interested on the issuing side
you can only use NG wallet and configure your own issuers into that and how can you do that it's again that simple thing
what uh because mimoto is a backend for the wallet right so what you have to do is in the mimoto ISS configurations you
can have your own uh issuers right based on this means instead of NG verify you
can have your own issuers well known whatever is you using in of
certifi okay but you have to follow the op for VC standard similarly there is no need to
even use the eign as authentication server you can have your own authentication server as
well it's just like in our ecosystem we are offering n as a stack completely so
we have all the modules including vol which is the holder issuer which is the
certify and the verification that is the in verify component and our code is interoperable so any verifier verify
component can use NG wallet and verify the VC generator that's the thing we are
working towards and achieving as well up to some extent there might be some scenarios or cases where verification is
not happening then we will be good and happy to uh so see those scenarios and
check what's the wrong happening then we can even enhance the support for that but we are looking for interoperability
from wallet side any issue can issue or any verifier can verify the
VC I hope it answer the question uh let me
just go to the next question is credential whatever we are giving is dummy data okay so it's not a dummy data
it basically what is happening is we have created a client ID right and uh
then the farmer ID we have created a farmer ID into the eate system so that
it can authenticate that user right and for the same farmer ID the data exist in the database it's something like you can
say uh I want to issue a educational certificate right I have a role number so that role number will be either
serving through some database or some something will be there maybe let's say Excel say it suppose right let's take an
example so I I want to use the kbi authentication which we showcased now you can enter your role number you can
enter your first name or date of birth and download my education certificate on the mobile wallet so for that certify
basically interact with the database okay whatever entry you see on the UI that gets verified through e signal
which is the authorization server and once it authenticate the certify qu is the database get the data convert into
VC and give it back to the wallet so so you can see maybe for the
demo dumy data but actually it's kind of a live D you have in the background which is the post Cas in our
case right yeah so that's the answer to that where the wallet is stored Sagar
has asked this question so I think wallet means uh he refering to the credentials right so on the mobile side
credential is stored within a like a what you say the local storage of the
mobile device it is encrypted okay so no one can just see the plain text if uh of the VC as well
and uh when you um go to the background and reload the applications you see the
VC again back from the uh storage itself so it's a local storage within the mobile
application and to encrypt and decrypt it we are using our own Library known as secure key
store which is helps to generate key Pairs and keys for the encryption decryptions and and other things so this
is being used for that key store management okay let's answer to that
question so let's I think for another one s is typing so I'll skip that part
there's one more question uh visha that is
about thanks uh for verify what is trust model and who can verify trust and not
trust so I'm not able to understand that like for the verify
okay um Sanji I'm I'm assuming U the trust is uh the credentials from what all
issuers do we trust so I'm I'm assuming um the question is on U what all issuers
we uh as a verify can trust right so right now we are just uh having a
workaround for this to have it in a trust list as a configuration uh which is taken in uh by in verify to identify
uh the valets that we trust uh and the issuers also uh but uh we we in our road
map we have a plan to also work on a trust framework or we will identify some good trust Frameworks and uh there is a
plan to integrate but uh all all those are are going to come only in the future
um since it's on the trust I also see Sassi in the call Sassi would like to would you like to add on the trust model
part how we are inging uh yeah I think there's lot of lot of of new things coming up in the market right now um
there is a framework um from glyph and Gan networks which which have come up
now uh wherein you could you could have a decentralized uh trust Registries and
you could you could Define some level of trust there uh there's also work going on with the governments to see how much
um uh the governments could also enable trust Registries uh so it it is in its
initial stage there is multiple things coming up um while while we are not
going to be choosing one versus another we would we would pretty much integrate everything uh out there
because it is a decentralized mode and it will continue that direction while the government as a regulatory body may
need certain times to verify some level of trust and put out that information so
we we doing both of it um as of now as I said there are two common protocols one
is blei and which is used by left and Gan networks and the other one is uh
dedi which is being promoted within India for decentralized uh directories
um so we will do both of it uh as of now trust is just modeled as you you pre
pre- know the keys of the issuer then you can you can put that information within our system that's how it's modeled while that's not the best but
that's that's what we are starting with yeah thank you
thank you um STI there's one more question please can you uh show how in
web configuration with Moto how do we connect sorry I was speaking on mute yes
so for NG web right let's go to the NG web code base again so NG web uh for the local setup
as I mentioned that start we are using web proxy right so web proxy is interacting with the mimoto so NG web
needs to know only about where the proxy is running now let's go to the proxy
code so how the proxy knows what is the environment of uh basically mimoto host
so if you see here I have mentioned mimoto as our local Dev environment right but I have not used that right I
have used my locally running mimoto so basically I have already done this mimoto for from the local compost
environment variable so here the proxy is interacting with the mimoto service
running on 189 19 19 Port and then this is the context PA of all the API
interacting with the mimoto right so proxy is running on 3010 proxy is
talking to mimoto and in web is talking to proxy only so in web is saying
okay reach out to the mimoto through proxy that is for local development only
but once you need a cloud everything is deployed in a one cluster so you can just access NG web Moto directly through
the service Discovery in the NG web you don't need to even expose outside as well for some things some internally
needed or you can also export through the API okay so yeah that's on the NG web
interaction with mimoto uh STI when um so this is because
of the local Docker setup correct where we go through proxy uh in the actual uh run between in
web and mimoto so it is just this configuration where you pointed to the
API yes can for our collab environment we have this host Expos for the mimoto
so it will be like V1 mimoto that's it okay hope that answered your question
because previously there was a similar question and uh I gave a text answer uh
I hope this clarifies thank you uh
okay there was one more question but I see Sashi is typing the answer
okay uh okay so which version they one more I'm just going from bottom because I see from Top people are answering
which version we can use for local setup and Link for repositories so basically okay let's
share all the repositories mentioned here we are on the latest version of NG in the Showcase I have used the latest
version which is about to release but you can use the only released versions for the stability side so I will just
share all the links here this is the mimoto repo you can directly refer to the main branch which is always uped
with the latest release or you can directly go to the release tag which is mentioned in the release section okay so this is the mimoto and
then we have NG web as well you can use that also and then for
the wallet we have mobile we have call it in the wallet that is for the mobile
all other if you're refering to certify and all you can direct just go to the MIP organizations and see other ref also
that we already sped last in the last works of the NG certify yeah so that's about
it what is the scope to combine Biometrics pH scan along with VC inside in the ecosystem and what libraries are
available so Biometrics and faces can during the VC download or so P scan uh or it is after
the download and when we do VC sharing maybe so I can just answer like first what we have today currently so once you
do a VC share right so somebody has asked about we have mentioned about offline VC sharing as well so how it
happens like I'll just show you through the application only yeah so what we have built is we
have built the verifier capability also in the NG itself if you go to set
you will see the option receive card and received card so you can have two instance of running in different
different devices one can act as a holder another one can act as a verifier so if you click on receive card it gives
you the uh QR code to scan suppose this is the verifier side okay you are seeing
this received card option now let's say you are on the wallet side so wallet has a option called share which does nothing
but scan that QR code once you scan that QR code okay the wallet this display all
the downloaded VC to be shared during the downloading the sharing the VC it ask you the option authenticate through
face verification it means the person who is sharing the VC
right and then after doing the face verification the face is getting match with the face of the VC So currently in
this demo we don't have a face if you see in the VC because we can't generate the that
big QR code containing the V uh phas on the mobile side so that's the ongoing
feature where we want to embed everything including face also in the QR code that's not supported right now in
the NG wallet that will come soon but once you have support this face is there
and you want to share the same VC so you can scan the face verify the face through the VC and then only can share
it so that also add that security like uh no one can share your VC without your
presence so that is like offline B as well so this is the one which I'm showing here it's
offline VC sharing through BL also on the face uh STI if you could
uh show the place where they can actually add in if they have SDK they can add
in okay so we right now we have integrated with the I scan SDK so I'll
just first go through the maybe specifications what we exposed there
so this is the face SDK specification so we are using Iris SDK so they have exposed one endpoint which says
configure where you can configure whatever the pr is to do the face verification and then you can use the
face compare uh function API interface Expos where you want to send whatever is
the current image captured and what is the VC image you have that does the comparison give you whether it is Meed
or not from threshold what is the threshold the threshold is part of your configurations okay let's see how to
integrate that in the code simply you want to replace it so I'll show this is the because we
have re application so we have used the npm module to use it for Android and iOS both so this is the
retive version of Iris can we are using it okay and it gives me a model file
which is like train data okay that train data is part of here if you see this TF flight
and uh how we are reading this and at what state let's show that
also I yeah so if you see initialize phas
model so let me see ini yeah so once you land on the
application first time after solution what we does is we keep early it was part of our file server now we have
bundled it through the application only so it was basically you have to initialize your face at the start of the
application only so here what we are saying is create the configurations this is the configurations we have created for this
SDK and then it basically configure and download this asset so what we are
seeing is earlier it was part of the API now it is bundle application so if it successfully initialized it will give us
the sucess if you initial it will initialization with fail if initiation get fail it means your face verification
will not fail oh sorry will not pass so that's the one thing uh you can use this uh like you can integrate any uh SDK you
want but it it has to be in this flow in the O TS there's a function called
initialize pH SDK model it can be either bundled within the application or through through some API that you can
make changes accordingly once you do that at what level we do the face verification
apption okay so it's like I as I mentioned during the VC sharing okay so VC sharing is happening
through share Machine request machine or
receive request from the verifier side scan machine
yeah so in the scan machine
Global will be faster scanner compare is used yeah so
because we are using retive this state now so it is achieved through event so
face compare is there yeah so capture image is used somewhere
so someone will be sending some event right so face
detected not less check this one face compare now this pH compare just give me
a minute I'm just going through the entire Cod just to explain you better come through uh scan machine
only we send some events
connecting scan not VP sharing connecting QR code sending St
event not show Q
this this one connecting start connection
and uh starting Connection in progress Target is in progress let's go
there and selecting VC we are selecting the VC that's why I mention we scan the QR code we select the VC so we are here
selecting the VC after selecting the VC it will ask for the verification yeah selected VC is there now once you go to
the section right so it will be in the scan action so that is done fine
so um very by and accept request so this is
basically sending by someone this event so let's see who sending this event so
scan machine is listening to this event fine but who is sending that this is
here yeah so if you see here this is the UI right so on the UI you see a VC has
been selected so there's a option which says button scan with face verification
when you click on that button that verify and accept request gets even gets scer right so that will be listened by
your scan machine and it will go to this page face verification consent when you are in
this state we will be exposing this state from the controller that enables
the face scan screen so uh somewhere we have be using face
scanner through some
condition okay so if you see there will be some conditional
here like credential exit and then only use this verifications you see verify identity overlay so somebody will be
using this verify identity overlay to R conditionally so it is still in the
scanning screen and the conditional will be somewhere mentioned through the
controller so these are the steps like scan screen is basically for the scan flow and the face scanner just to
display that capturing the opening the camera capturing the face and giving the control back to the machine so once you
get into the machine it comes like this consent is given let's say we show a down whether you like accept the user
consent like we are capturing your photo and once uh that's done it goes to verify identity and verify identity
basically opens the face scanner Page open the camera scan the ph and when face is verified successfully we send
this face value event and it's it start sending the VC to the receiver
side so that's the end to end flow basically you have to first load the um
face SDK model at the start of the application then through the sharing flow wherever you want to use that
feature that is exposed UI exposed through face scanner PSX file and the state machine is managed by the scan
machine I hope it answers the question
okay so how many questions left do we have much thanks I see um s mentioned to
IO we have answered right yeah yeah I think last one is can
you demonstrate the IDC client onboarding and p12 file creation okay so I'll just go to the documentation only
so these are the steps mentioned here create new client ID on boarding mot as a YDC client so basically what we have
done for our simplification we have one jip file which is not uploaded here but we can share it later as well so this
jip file is like single kind of bundle which helps you to create a client ID
and as well as P2 file out of it once you run that you will get all the public key client uh clientas and the key P
generation done once you have that generation done you can use so we are
using our e Signet service for the ID because we are using e sign for authentication this is the end point for E Signet client creation this is the
request body for thec client you can choose any name you want to give client name you can choose any you want to give
public key is one what is which is generated the step number one user claims is basically to Define which uh
claims you want to access through this IDC client this all context reference is nothing but the a value which defines
the way of user can lo as somebody has asked question like what is this kbii and all so basically
biometric is you can login through biometric knowledge is you can have knowledge Base information like we showcase through farmer ID first name
last name date of birth generated code is nothing but the OTP base it can be like you can have some unique identifier
like your Adar number in India or some social security number somewhere whatever you use for the credential ID
and mobile number or email link to that number can get the OTP and you can authenticate linked wallet is a feature
which basically allows you to login on the ring party through a Signet so that when I was showcasing this uh different
ways of authentication so you see we have this link with in mobile app basically what you can do is you can
click on this the session is expired because I've open it for a long
time so you can sign with e Signet you can click on this and you can just scan
this QR code let me share whether I have this open
because this QR code is not valid for this particular domain which I'm sending so that's why it is seeing QR code but
it is scanning and if you scan then QR code will allow you to log into that thing so let me just check whether uh
that is working or not right now but this is basically for the national identification National identifier
number we do this wallet based login that is also one of the ACR we have so
can afford these kind of authentications logo URL is the one which you on the UI
Bally this one if you if you have noticed when I was downloading the VC we could see e signat is interacting with
the NG wallet so that's the logo URL redirect urri we have mentioned here a few so this is the fixed one for the
NG wallet which is our application next you can have any number of R depends on
where are using so this is one of the collab environment in G we have deployed and if you want to use your local setup
also so we can use that also so I can show you for the local setup I am running uh V web on local 330 so I'll
just change to
the collection so we running out of time as well quickly sorry
yeah yeah if you have answered most of the
questions then good uh I think we can continue to have uh Communications
in the community community site
yeah yes S I have also shared the link here so for any further questions uh you
all can reach to us through the community link is shared here and the recording of the session will also be
uploaded there so feel free to access
it okay okay cool thank you thank you everyone for the session I hope it was
good you could follow the steps thank you STI thank you everyone for joining
[Music]



Questions from 18 November Workshop:\


1. What DID methods are currently supported?
2. How will we get the p12 file when creating oidc client?
3. How to configure mimoto in inji-web?
4. Will how credentials are stored and secured in web/mobile wallet be covered?
5. In a real-world deployment, which party configures (binds) various issuers so they are visible via the wallet?
6. Is it the service provider helping on-board the issuer?
7. Inji-web and verify is available only in the collab env? Or if any other env please share the link.
8. Keys, signatures, and proofs - can blockchain be used instead of traditional RDBMS within the context of Inji ecosystem?
9. Please once config mimoto for inji web. Whenever we are trying to do it, we are facing issues.
10. How is the credential validation happening?
11. Is VC following the W3C data model?
12. Also, when the farmerId was entered to download credentials, how is authentication with the end user happening?
13. For verify, what is the trust model? Who can verify trust/not trust?
14. Is it required to use Inji wallet with Inji certify and verify? Or can they stand on their own?
15. Is the credential whatever we are giving dummy data?
16. Where is the wallet stored?
17. There is a feature mentioned in the repository readme "Conduct offline face authentication." Can you give more details on how it works and what it uses?
18. Can you demonstrate oidc client onboarding and p12 file creation?
19. Please can you show once Inji-web configuration with mimoto? How do we connect?
20. Any scope to run AI agents for selective disclosure on top of Inji wallet where Inji wallet can provide SDK functionalities to develop various AI agents?





FAQs about Inji : MOSIP’s Digital Credentialing Stack
