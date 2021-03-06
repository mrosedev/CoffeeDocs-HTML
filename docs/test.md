---
layout : default
---


<meta name="DC.Title" content="XML Digital Signature API Overview and Tutorial" />
<meta name="abstract" content="" />
<meta name="description" content="" />
<meta name="DC.Format" content="XHTML" />
<meta name="DC.Identifier" content="GUID-DB46A001-6DBD-4571-BDBC-1BBC394BF61E" />



<title>XML Digital Signature API Overview and Tutorial</title>

<meta name="doctitle" content="12 XML Digital Signature API Overview and Tutorial&#xA;" />
<meta name="date" content="2018-04-19T11:46:47Z" />
<meta name="robots" content="noarchive" />
<meta name="relnum" content="Release 11" />
<meta name="partnum" content="E94828-01" />
<meta name="docid" content="JSSEC" />


<link rel="contents" href="toc.htm" title="Contents" type="text/html" />
<link rel="prev" href="java-sasl-api-programming-and-deployment-guide1.htm" title="Previous" type="text/html" />
<link rel="next" href="security-api-specification1.htm" title="Next" type="text/html" />
</head>
<body>
<div class="header"><a id="top" name="top"></a>
<div class="zz-skip-header"><a href="#BEGIN">Go to primary content</a></div>
<table class="simple oac_no_warn" summary="" cellspacing="0" cellpadding="0" width="100%">
<tr>
<td valign="top"><b>Java Platform, Standard Edition Security Developer&#8217;s Guide</b><br />
<b>
<span>Release 11</span> 
</b><br />
E94828-01
</td>
<td valign="bottom" align="right">
<table class="simple oac_no_warn" summary="" cellspacing="0" cellpadding="0" width="225">
<tr>
<td> </td>
<td align="center" valign="top">
<a href="toc.htm"><img src="../../dcommon/gifs/toc.gif" alt="Go To Table Of Contents" /><br />
<span class="icon">Contents</span></a>
</td>
</tr>
</table>
</td>
</tr>
</table>
<hr />
<table class="simple oac_no_warn" summary="" cellspacing="0" cellpadding="0" width="100">
<tr>
<td align="center">
<a href="java-sasl-api-programming-and-deployment-guide1.htm">
<img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span>
</a>
</td>
<td align="center">
<a href="security-api-specification1.htm">
<img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span>
</a>
</td>
<td> </td>
</tr>
</table>
<a name="BEGIN" id="BEGIN"></a></div><!-- class="header" -->
<div class="ind"><a id="GUID-DB46A001-6DBD-4571-BDBC-1BBC394BF61E" name="GUID-DB46A001-6DBD-4571-BDBC-1BBC394BF61E"></a><!-- End Header -->
<h1 id="JSSEC-GUID-DB46A001-6DBD-4571-BDBC-1BBC394BF61E" class="sect1"><span class="enumeration_chapter">12 </span>XML Digital Signature API Overview and Tutorial</h1>
<div><p></p>
  
The Java XML Digital Signature API is a **`standard`** Java API for generating and validating XML Signatures. This API was defined under the Java Community Process as <a href="http://www.jcp.org/en/jsr/detail?id=105" target="_blank">JSR 105</a>.

<p>XML Signatures can be applied to data of any type, XML or binary (see <a href="http://www.w3.org/TR/xmldsig-core/" target="_blank">XML Signature Syntax and Processing</a>). The resulting signature is represented in XML. An XML Signature can be used to secure your data and provide data integrity, message authentication, and signer authentication.</p>
<p>After providing a brief overview of XML Signatures and the XML Digital Signature API, this document presents two examples that demonstrate how to use the API to validate and generate an XML Signature. This document assumes that you have a basic knowledge of cryptography and digital signatures.</p>
<p>The API is designed to support all of the required or recommended features of the W3C Recommendation for XML-Signature Syntax and Processing. The API is extensible and pluggable and is based on the Java Cryptography Service Provider Architecture; see <a href="java-cryptography-architecture-jca-reference-guide.htm#GUID-2BCFDD85-D533-4E6C-8CE9-29990DEB0190" title='The Java Cryptography Architecture (JCA) is a major piece of the platform, and contains a "provider" architecture and a set of APIs for digital signatures, message digests (hashes), certificates and certificate validation, encryption (symmetric/asymmetric block/stream ciphers), key generation and management, and secure random number generation, to name a few.'>Java Cryptography Architecture (JCA) Reference Guide</a>. The API is designed for two types of developers:</p>
<ul style="list-style-type: disc;"><li>Developers who want to use the XML Digital Signature API to generate and validate XML signatures</li>
<li>Developers who want to create a concrete implementation of the XML Digital Signature API and register it as a cryptographic service of a JCA provider (see <a href="java-cryptography-architecture-jca-reference-guide.htm#GUID-D8E30FE5-66B4-4F6A-88B7-280789E68307" title="In order to be used, a cryptographic provider must first be installed, then registered either statically or dynamically. There are a variety of Sun providers shipped with this release (SUN, SunJCE, SunJSSE, SunRsaSign, etc.) that are already installed and registered. The following sections describe how to install and register additional providers.Each Provider class instance has a (currently case-sensitive) name, a version number, and a string description of the provider and its services.">The Provider Class</a>).</li>
</ul>
</div>
<div class="sect2"><a id="GUID-BBFA7B90-3EA2-49DE-964B-8A60D4134343" name="GUID-BBFA7B90-3EA2-49DE-964B-8A60D4134343"></a><h2 id="JSSEC-GUID-BBFA7B90-3EA2-49DE-964B-8A60D4134343" class="sect2">Package Hierarchy</h2>
<div><p></p>
<p>The following six packages, which are contained in the <a href="https://docs.oracle.com/javase/10/docs/api/java.xml.crypto-summary.html" target="_blank"><span class="apiname">java.xml.crypto</span></a> module, comprise the XML Digital Signature API:</p>
<ul style="list-style-type: disc;"><li><span class="apiname">javax.xml.crypto</span></li>
<li><span class="apiname">javax.xml.crypto.dsig</span></li>
<li><span class="apiname">javax.xml.crypto.dsig.keyinfo</span></li>
<li><span class="apiname">javax.xml.crypto.dsig.spec</span></li>
<li><span class="apiname">javax.xml.crypto.dom</span></li>
<li><span class="apiname">javax.xml.crypto.dsig.dom</span></li>
</ul>
<p>The <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/package-summary.html" target="_blank"><span class="apiname">javax.xml.crypto</span></a> package contains common classes that are used to perform XML cryptographic operations, such as generating an XML signature or encrypting XML data. Two notable classes in this package are the <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/KeySelector.html" target="_blank"><span class="apiname">KeySelector</span></a> class, which allows developers to supply implementations that locate and optionally validate keys using the information contained in a <span class="apiname">KeyInfo</span> object, and the <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/URIDereferencer.html" target="_blank"><span class="apiname">URIDereferencer</span></a> class, which allows developers to create and specify their own URI dereferencing implementations.</p>
<p>The <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/package-summary.html" target="_blank"><span class="apiname">javax.xml.crypto.dsig</span></a> package includes interfaces that represent the core elements defined in the W3C XML digital signature specification. Of primary significance is the <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/XMLSignature.html" target="_blank"><span class="apiname">XMLSignature</span></a> class, which allows you to sign and validate an XML digital signature. Most of the XML signature structures or elements are represented by a corresponding interface (except for the KeyInfo structures, which are included in their own package and are discussed in the next paragraph). These interfaces include: <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/SignedInfo.html" target="_blank"><span class="apiname">SignedInfo</span></a>, <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/CanonicalizationMethod.html" target="_blank"><span class="apiname">CanonicalizationMethod</span></a>, <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/SignatureMethod.html" target="_blank"><span class="apiname">SignatureMethod</span></a>, <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/Reference.html" target="_blank"><span class="apiname">Reference</span></a>, <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/Transform.html" target="_blank"><span class="apiname">Transform</span></a>, <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/DigestMethod.html" target="_blank"><span class="apiname">DigestMethod</span></a>, <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/XMLObject.html" target="_blank"><span class="apiname">XMLObject</span></a>, <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/Manifest.html" target="_blank"><span class="apiname">Manifest</span></a>, <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/SignatureProperty.html" target="_blank"><span class="apiname">SignatureProperty</span></a>, and <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/SignatureProperties.html" target="_blank"><span class="apiname">SignatureProperties</span></a>. The <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/XMLSignatureFactory.html" target="_blank"><span class="apiname">XMLSignatureFactory</span></a> class is an abstract factory that is used to create objects that implement these interfaces.</p>
<p>The <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/package-summary.html" target="_blank"><span class="apiname">javax.xml.crypto.dsig.keyinfo</span></a> package contains interfaces that represent most of the <span class="apiname">KeyInfo</span> structures defined in the W3C XML digital signature recommendation, including <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/KeyInfo.html" target="_blank"><span class="apiname">KeyInfo</span></a>, <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/KeyName.html" target="_blank"><span class="apiname">KeyName</span></a>, <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/KeyValue.html" target="_blank"><span class="apiname">KeyValue</span></a>, <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/X509Data.html" target="_blank"><span class="apiname">X509Data</span></a>, <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/X509IssuerSerial.html" target="_blank"><span class="apiname">X509IssuerSerial</span></a>, <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/RetrievalMethod.html" target="_blank"><span class="apiname">RetrievalMethod</span></a>, and <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/PGPData.html" target="_blank"><span class="apiname">PGPData</span></a>. The <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/KeyInfoFactory.html" target="_blank"><span class="apiname">KeyInfoFactory</span></a> class is an abstract factory that is used to create objects that implement these interfaces.</p>
<p>The <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/spec/package-summary.html" target="_blank"><span class="apiname">javax.xml.crypto.dsig.spec</span></a> package contains interfaces and classes representing input parameters for the digest, signature, transform, or canonicalization algorithms used in the processing of XML signatures.</p>
<p>Finally, the <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dom/package-summary.html" target="_blank"><span class="apiname">javax.xml.crypto.dom</span></a> and <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/dom/package-summary.html" target="_blank"><span class="apiname">javax.xml.crypto.dsig.dom</span></a> packages contains DOM-specific classes for the <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/package-summary.html" target="_blank"><span class="apiname">javax.xml.crypto</span></a> and <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/package-summary.html" target="_blank"><span class="apiname">javax.xml.crypto.dsig</span></a> packages, respectively. Only developers and users who are creating or using a DOM-based <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/XMLSignatureFactory.html" target="_blank"><span class="apiname">XMLSignatureFactory</span></a> or <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/KeyInfoFactory.html" target="_blank"><span class="apiname">KeyInfoFactory</span></a> implementation will need to make direct use of these packages.</p>
</div>
</div>
<div class="sect2"><a id="GUID-A32C5AC5-08F9-4316-9D63-0CDEAC3A5405" name="GUID-A32C5AC5-08F9-4316-9D63-0CDEAC3A5405"></a><h2 id="JSSEC-GUID-A32C5AC5-08F9-4316-9D63-0CDEAC3A5405" class="sect2">Service Providers</h2>
<div><p></p>
<p>A Java XML Signature is a concrete implementation of the abstract <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/XMLSignatureFactory.html" target="_blank"><span class="apiname">XMLSignatureFactory</span></a> and <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/KeyInfoFactory.html" target="_blank"><span class="apiname">KeyInfoFactory</span></a> classes and is responsible for creating objects and algorithms that parse, generate and validate XML Signatures and <span class="apiname">KeyInfo</span> structures. A concrete implementation of <span class="apiname">XMLSignatureFactory</span> must provide support for each of the required algorithms as specified by the W3C recommendation for XML Signatures. It can optionally support other algorithms as defined by the W3C recommendation or other specifications.</p>
<p>The Java XML Digital Signature API leverages the JCA provider model for registering and loading <span class="apiname">XMLSignatureFactory</span> and <span class="apiname">KeyInfoFactory</span> implementations.</p>
<p>Each concrete <span class="apiname">XMLSignatureFactory</span> or <span class="apiname">KeyInfoFactory</span> implementation supports a specific XML mechanism type that identifies the XML processing mechanism that an implementation uses internally to parse and generate XML signature and <span class="apiname">KeyInfo</span> structures. This JSR supports one standard type, DOM. The XML Digital Signature provider implementation that is bundled with the JDK supports the DOM mechanism.</p>
<p>An XML Digital Signature API implementation should use underlying JCA engine classes, such as <a href="https://docs.oracle.com/javase/10/docs/api/java/security/Signature.html" target="_blank"><span class="apiname">java.security.Signature</span></a> and <a href="https://docs.oracle.com/javase/10/docs/api/java/security/MessageDigest.html" target="_blank"><span class="apiname">java.security.MessageDigest</span></a>, to perform cryptographic operations.</p>
<p>In addition to the <span class="apiname">XMLSignatureFactory</span> and <span class="apiname">KeyInfoFactory</span> classes, JSR 105 supports a service provider interface for transform and canonicalization algorithms. The <a href="https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/TransformService.html" target="_blank"><span class="apiname">TransformService</span></a> class allows you to develop and plug in an implementation of a specific transform or canonicalization algorithm for a particular XML mechanism type. The <span class="apiname">TransformService</span> class uses the standard JCA provider model for registering and loading implementations. Each JSR 105 implementation should use the <span class="apiname">TransformService</span> class to find a provider that supports transform and canonicalization algorithms in XML Signatures that it is generating or validating.</p>
</div>
</div>
<div class="sect2"><a id="GUID-E11E6051-5F30-4DDA-A4EE-5F9C1AB1F7B8" name="GUID-E11E6051-5F30-4DDA-A4EE-5F9C1AB1F7B8"></a><h2 id="JSSEC-GUID-E11E6051-5F30-4DDA-A4EE-5F9C1AB1F7B8" class="sect2">Introduction to XML Signatures</h2>
<div><p></p>
<p>You can use an XML Signature to sign any arbitrary data, whether it is XML or binary. The data is identified via URIs in one or more Reference elements. XML Signatures are described in one or more of three forms: detached, enveloping, or enveloped. A detached signature is over data that is external, or outside of the signature element itself. Enveloping signatures are signatures over data that is inside the signature element, and an enveloped signature is a signature that is contained inside the data that it is signing.</p>
</div>
<div class="sect3"><a id="GUID-E5A89234-A67A-4999-8E31-6D6C26B9BAAF" name="GUID-E5A89234-A67A-4999-8E31-6D6C26B9BAAF"></a><h3 id="JSSEC-GUID-E5A89234-A67A-4999-8E31-6D6C26B9BAAF" class="sect3">Example of an XML Signature</h3>
<div><p></p>
<p>The easiest way to describe the contents of an XML Signature is to show an actual sample and describe each component in more detail. <a href="java-xml-digital-signature-api-overview-and-tutorial.htm#GUID-22AB40C4-45EC-4714-91A2-CFB59EC05AA0__GUID-4DCD9F0B-02C7-4C00-AB66-096C7F262ACF">Example 12-3</a> is an enveloped XML Signature generated over the contents of an XML document. The root element, <code class="codeph">Envelop</code>, contains a <code class="codeph">Signature</code> element:</p>
<pre class="oac_no_warn" dir="ltr">&lt;Envelope xmlns="urn:envelope"&gt;
  &lt;Signature xmlns="http://www.w3.org/2000/09/xmldsig#"&gt;
    &lt;!-- ... --&gt;
  &lt;/Signature&gt;
&lt;/Envelope&gt; </pre>
<p>This <code class="codeph">Signature</code> element has been inserted inside the content that it is signing, thereby making it an enveloped signature. The required <code class="codeph">SignedInfo</code> element contains the information that is actually signed:</p>
<pre class="oac_no_warn" dir="ltr">&lt;Envelope xmlns="urn:envelope"&gt;
  &lt;Signature xmlns="http://www.w3.org/2000/09/xmldsig#"&gt;
    &lt;SignedInfo&gt;
      &lt;CanonicalizationMethod Algorithm="http://www.w3.org/TR/2001/REC-xml-c14n-20010315#WithComments"/&gt;
      &lt;SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"/&gt;
      &lt;Reference URI=""&gt;
        &lt;Transforms&gt;
          &lt;Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/&gt;
        &lt;/Transforms&gt;
        &lt;DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256"/&gt;
        &lt;DigestValue&gt;/juoQ4bDxElf1M+KJauO20euW+QAvvPP0nDCruCQooM=&lt;/DigestValue&gt;
      &lt;/Reference&gt;
    &lt;/SignedInfo&gt;
    &lt;!-- ... --&gt;
  &lt;/Signature&gt;
&lt;/Envelope&gt; </pre>
<p></p>
<p>The required <code class="codeph">CanonicalizationMethod</code> element defines the algorithm used to canonicalize the <code class="codeph">SignedInfo</code> element before it is signed or validated. Canonicalization is the process of converting XML content to a canonical form, to take into account changes that can invalidate a signature over that data. Canonicalization is necessary due to the nature of XML and the way it is parsed by different processors and intermediaries, which can change the data such that the signature is no longer valid but the signed data is still logically equivalent.</p>
<p>The required <code class="codeph">SignatureMethod</code> element defines the digital signature algorithm used to generate the signature, in this case RSA with SHA-256.</p>
<p>One or more <code class="codeph">Reference</code> elements identify the data that is digested. Each <code class="codeph">Reference</code> element identifies the data via a URI. In this example, the value of the URI is the empty String (""), which indicates the root of the document. The optional <code class="codeph">Transforms</code> element contains a list of one or more <code class="codeph">Transform</code> elements, each of which describes a transformation algorithm used to transform the data before it is digested. In this example, there is one Transform element for the enveloped transform algorithm. The enveloped transform is required for enveloped signatures so that the signature element itself is removed before calculating the signature value. The required <code class="codeph">DigestMethod</code> element defines the algorithm used to digest the data, in this case SHA-256. Finally the required <code class="codeph">DigestValue</code> element contains the actual base64-encoded digested value.</p>
<p>The required <code class="codeph">SignatureValue</code> element contains the base64-encoded signature value of the signature over the <code class="codeph">SignedInfo</code> element.</p>
<p>The optional <code class="codeph">KeyInfo</code> element contains information about the key that is needed to validate the signature:</p>
<pre class="oac_no_warn" dir="ltr">    &lt;KeyInfo&gt;
      &lt;KeyValue&gt;
        &lt;RSAKeyValue&gt;
          &lt;Modulus&gt;
9hSmAKw/4TTw/1l1u1pYzdFm6lOjRB/5NfdGWl/fB8iAa/tiK0f1u/VWoK6SMtogYgSDKqQThbAu
9dy9rRnOWRGY2He1JtpOvGh0WCmIFUEs2P22HvEf+JGKVEpkoP4hv53ucT69T+7nKGK3/bjxgp+T
C7fbnVj651+jAHuDFlC8Txt1R8ZymfN5cUeHIH96dvNFrtai/uwZDbVMfhV9chL//+Vyhx4O5nHv
jfS+0So9Qi52YAbEyLu6+BLdu8wnMWapC88CfXsRwrpx8b6aCU0e6QSZyOvdgXWz3+9ifVTBDIxE
kjhL5OASx0qjvc+dPUOMvq7fJE05RRZLyb0YJw==
          &lt;/Modulus&gt;
          &lt;Exponent&gt;AQAB&lt;/Exponent&gt;
        &lt;/RSAKeyValue&gt;
      &lt;/KeyValue&gt;
    &lt;/KeyInfo&gt;</pre>
<p>This <code class="codeph">KeyInfo</code> element contains a <code class="codeph">KeyValue</code> element, which in turn contains a <code class="codeph">RSAKeyValue</code> element consisting of the public key needed to validate the signature. <code class="codeph">KeyInfo</code> can contain various content such as X.509 certificates and PGP key identifiers. See <a href="http://www.w3.org/TR/xmldsig-core/#sec-KeyInfo" target="_blank">The <code class="codeph">KeyInfo</code> Element</a> in <a href="https://www.w3.org/TR/xmldsig-core/" target="_blank">XML Signature Syntax and Processing</a> for more information on the different <code class="codeph">KeyInfo</code> types.</p>
</div>
</div>
</div>
<div class="sect2"><a id="GUID-8618C294-3BFE-45C3-9A1E-C4629E337E68" name="GUID-8618C294-3BFE-45C3-9A1E-C4629E337E68"></a><h2 id="JSSEC-GUID-8618C294-3BFE-45C3-9A1E-C4629E337E68" class="sect2">XML Signature Secure Validation Mode</h2>
<div><p>XML Signature secure validation mode can protect you from XML Signatures that may contain potentially hostile constructs that can cause denial-of-service or other types of security issues.</p>
<p>XML Signature secure validation mode is enabled by default when you run your application with a security manager.</p>
<p>You can also enable XML Signature secure validation mode by setting the <code class="codeph">org.jcp.xml.dsig.secureValidation</code> property to <code class="codeph">TRUE</code>. You must set this property to <code class="codeph">TRUE</code> before validating an XML Signature.</p>
<p> To set this property in an application, call the <span class="apiname">javax.xml.crypto.dsig.dom.DOMValidateContext.setProperty</span> method:</p>
<pre class="oac_no_warn" dir="ltr">    DOMValidateContext context = new DOMValidateContext(key, element);
    context.setProperty("org.jcp.xml.dsig.secureValidation", Boolean.TRUE);</pre>
<p>When XML Signature secure validation mode is enabled, XML Signatures are processed more securely. Limits are set on various XML Signature constructs to avoid conditions such as denial-of-service attacks. By default, it enforces the following restrictions:</p>
<ul style="list-style-type: disc;"><li>Forbids the use of XSLT transforms</li>
<li>Restricts the number of <code class="codeph">SignedInfo</code> or <code class="codeph">Manifest</code> <code class="codeph">Reference</code> elements to 30 or less</li>
<li>Restricts the number of <code class="codeph">Reference</code> transforms to 5 or less</li>
<li>Forbids the use of MD5-related signatures or MAC algorithms</li>
<li>Ensures that <code class="codeph">Reference</code> IDs are unique to help prevent signature wrapping attacks</li>
<li>Forbids <code class="codeph">Reference</code> URIs of type <code class="codeph">http</code>, <code class="codeph">https</code>, or <code class="codeph">file</code></li>
<li>Does not allow a <code class="codeph">RetrievalMethod</code> element to reference another <code class="codeph">RetrievalMethod</code> element</li>
<li>Forbids RSA or DSA keys less than 1024 bits</li>
</ul>
<p>In addition, you can use the <code class="codeph">jdk.xml.dsig.secureValidationPolicy</code> Security Property to control and fine-tune the restrictions listed previously or add additional restrictions. See the definition of this Security Property in the <code>java.security</code> file for more information.</p>
</div>
</div>
<div class="sect2"><a id="GUID-E7E9239F-C973-4D05-AC3F-53F714C259DB" name="GUID-E7E9239F-C973-4D05-AC3F-53F714C259DB"></a><h2 id="JSSEC-GUID-E7E9239F-C973-4D05-AC3F-53F714C259DB" class="sect2">XML Digital Signature API Examples</h2>
<div><p></p>
<p>The following sections describe two examples that show how to use the XML Digital Signature API:</p>
</div>
<div class="sect3"><a id="GUID-22AB40C4-45EC-4714-91A2-CFB59EC05AA0" name="GUID-22AB40C4-45EC-4714-91A2-CFB59EC05AA0"></a><h3 id="JSSEC-GUID-22AB40C4-45EC-4714-91A2-CFB59EC05AA0" class="sect3">Validate Example</h3>
<div><p></p>
<p>To compile and run the example, execute the following commands:</p>
<pre class="oac_no_warn" dir="ltr">$ javac Validate.java 
$ java Validate signature.xml</pre>
<p>The sample program will validate the signature in the file <code>signature.xml</code> in the current working directory.</p>
<div class="example" id="GUID-22AB40C4-45EC-4714-91A2-CFB59EC05AA0__GUID-CCB8BC57-84D6-4EC2-A81A-A9760B4CD190"><p class="titleinexample">Example 12-1 Validate.java</p><pre class="oac_no_warn" dir="ltr">import javax.xml.crypto.*;
import javax.xml.crypto.dsig.*;
import javax.xml.crypto.dom.*;
import javax.xml.crypto.dsig.dom.DOMValidateContext;
import javax.xml.crypto.dsig.keyinfo.*;
import java.io.FileInputStream;
import java.security.*;
import java.util.Collections;
import java.util.Iterator;
import java.util.List;
import javax.xml.parsers.DocumentBuilderFactory;
import org.w3c.dom.Document;
import org.w3c.dom.NodeList;

/**
 * This is a simple example of validating an XML Signature using
 * the XML Signature API. It assumes the key needed to validate
 * the signature is contained in a KeyValue KeyInfo.
 */
public class Validate {

    //
    // Synopsis: java Validate [document]
    //
    //    where "document" is the name of a file containing the XML document
    //    to be validated.
    //
    public static void main(String[] args) throws Exception {

        // Instantiate the document to be validated
        DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
        dbf.setNamespaceAware(true);
        Document doc = null;
        try (FileInputStream fis = new FileInputStream(args[0])) {
            doc = dbf.newDocumentBuilder().parse(fis);
        }

        // Find Signature element
        NodeList nl =
            doc.getElementsByTagNameNS(XMLSignature.XMLNS, "Signature");
        if (nl.getLength() == 0) {
            throw new Exception("Cannot find Signature element");
        }

        // Create a DOM XMLSignatureFactory that will be used to unmarshal the
        // document containing the XMLSignature
        XMLSignatureFactory fac = XMLSignatureFactory.getInstance("DOM");

        // Create a DOMValidateContext and specify a KeyValue KeySelector
        // and document context
        DOMValidateContext valContext = new DOMValidateContext
            (new KeyValueKeySelector(), nl.item(0));

        // unmarshal the XMLSignature
        XMLSignature signature = fac.unmarshalXMLSignature(valContext);

        // Validate the XMLSignature (generated above)
        boolean coreValidity = signature.validate(valContext);

        // Check core validation status
        if (coreValidity == false) {
            System.err.println("Signature failed core validation");
            boolean sv = signature.getSignatureValue().validate(valContext);
            System.out.println("signature validation status: " + sv);
            // check the validation status of each Reference
            Iterator&lt;Reference&gt; i =
                signature.getSignedInfo().getReferences().iterator();
            for (int j=0; i.hasNext(); j++) {
                boolean refValid = i.next().validate(valContext);
                System.out.println("ref["+j+"] validity status: " + refValid);
            }
        } else {
            System.out.println("Signature passed core validation");
        }
    }

    /**
     * KeySelector which retrieves the public key out of the
     * KeyValue element and returns it.
     * NOTE: If the key algorithm doesn't match signature algorithm,
     * then the public key will be ignored.
     */
    private static class KeyValueKeySelector extends KeySelector {
        public KeySelectorResult select(KeyInfo keyInfo,
                                        KeySelector.Purpose purpose,
                                        AlgorithmMethod method,
                                        XMLCryptoContext context)
            throws KeySelectorException {
            if (keyInfo == null) {
                throw new KeySelectorException("Null KeyInfo object!");
            }
            SignatureMethod sm = (SignatureMethod) method;
            List&lt;XMLStructure&gt; list = keyInfo.getContent();

            for (int i = 0; i &lt; list.size(); i++) {
                XMLStructure xmlStructure = list.get(i);
                if (xmlStructure instanceof KeyValue) {
                    PublicKey pk = null;
                    try {
                        pk = ((KeyValue)xmlStructure).getPublicKey();
                    } catch (KeyException ke) {
                        throw new KeySelectorException(ke);
                    }
                    // make sure algorithm is compatible with method
                    if (algEquals(sm.getAlgorithm(), pk.getAlgorithm())) {
                        return new SimpleKeySelectorResult(pk);
                    }
                }
            }
            throw new KeySelectorException("No KeyValue element found!");
        }

        static boolean algEquals(String algURI, String algName) {
            if (algName.equalsIgnoreCase("DSA") &amp;&amp;
                algURI.equalsIgnoreCase("http://www.w3.org/2009/xmldsig11#dsa-sha256")) {
                return true;
            } else if (algName.equalsIgnoreCase("RSA") &amp;&amp;
                       algURI.equalsIgnoreCase("http://www.w3.org/2001/04/xmldsig-more#rsa-sha256")) {
                return true;
            } else {
                return false;
            }
        }
    }

    private static class SimpleKeySelectorResult implements KeySelectorResult {
        private PublicKey pk;
        SimpleKeySelectorResult(PublicKey pk) {
            this.pk = pk;
        }

        public Key getKey() { return pk; }
    }
}
</pre>
</div>
<!-- class="example" -->
<div class="example" id="GUID-22AB40C4-45EC-4714-91A2-CFB59EC05AA0__GUID-A82408FF-EC50-46A6-8D22-3B06B85AB588"><p class="titleinexample">Example 12-2 envelope.xml</p><pre class="oac_no_warn" dir="ltr">&lt;Envelope xmlns="urn:envelope"&gt;
&lt;/Envelope&gt;</pre>
</div>
<!-- class="example" -->
<div class="example" id="GUID-22AB40C4-45EC-4714-91A2-CFB59EC05AA0__GUID-4DCD9F0B-02C7-4C00-AB66-096C7F262ACF"><p class="titleinexample">Example 12-3 signature.xml</p><p>This file has been indented and formatted for readability.</p>
<pre class="oac_no_warn" dir="ltr">&lt;?xml version="1.0" encoding="UTF-8" standalone="no"?&gt;
&lt;Envelope xmlns="urn:envelope"&gt;
  &lt;Signature xmlns="http://www.w3.org/2000/09/xmldsig#"&gt;
    &lt;SignedInfo&gt;
      &lt;CanonicalizationMethod Algorithm="http://www.w3.org/TR/2001/REC-xml-c14n-20010315#WithComments"/&gt;
      &lt;SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"/&gt;
      &lt;Reference URI=""&gt;
        &lt;Transforms&gt;
          &lt;Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/&gt;
        &lt;/Transforms&gt;
        &lt;DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256"/&gt;
        &lt;DigestValue&gt;/juoQ4bDxElf1M+KJauO20euW+QAvvPP0nDCruCQooM=&lt;/DigestValue&gt;
      &lt;/Reference&gt;
    &lt;/SignedInfo&gt;
    &lt;SignatureValue&gt;
Vorr4nABCD7eWOjh4jn8pdM5iseGJPt4BmlgjEbxr05TsR9ObHq7WLVOBOtJfb3M6pXv6NnTucpH
e/97zHbuUMaNeGxCs/gN7YDUGOkQE1Gs4HAbGwXuTcif3pw+066ZW4uxyzapwS6lZHmqIm7PRl8I
NIQXVL4dezLe+rx77Kh+rZRheVe4UlTTP+TmIOaBZo93GQ5FudreMhSiuIC0Nx2SP7mAkt6+8kVH
luZouFbqriSvyhzIxDgyOXpm/PHCuuPU2scCokwjEZBtlZXDOl6lIWGllnyrptWntQ6F/ngQObI5
c2+npgCshq1svGuS/xx18MAFHGWi98Vj+07QCg==
    &lt;/SignatureValue&gt;
    &lt;KeyInfo&gt;
      &lt;KeyValue&gt;
        &lt;RSAKeyValue&gt;
          &lt;Modulus&gt;
9hSmAKw/4TTw/1l1u1pYzdFm6lOjRB/5NfdGWl/fB8iAa/tiK0f1u/VWoK6SMtogYgSDKqQThbAu
9dy9rRnOWRGY2He1JtpOvGh0WCmIFUEs2P22HvEf+JGKVEpkoP4hv53ucT69T+7nKGK3/bjxgp+T
C7fbnVj651+jAHuDFlC8Txt1R8ZymfN5cUeHIH96dvNFrtai/uwZDbVMfhV9chL//+Vyhx4O5nHv
jfS+0So9Qi52YAbEyLu6+BLdu8wnMWapC88CfXsRwrpx8b6aCU0e6QSZyOvdgXWz3+9ifVTBDIxE
kjhL5OASx0qjvc+dPUOMvq7fJE05RRZLyb0YJw==
          &lt;/Modulus&gt;
          &lt;Exponent&gt;AQAB&lt;/Exponent&gt;
        &lt;/RSAKeyValue&gt;
      &lt;/KeyValue&gt;
    &lt;/KeyInfo&gt;
  &lt;/Signature&gt;
&lt;/Envelope&gt;</pre>
</div>
<!-- class="example" -->
</div>
<div class="sect4"><a id="GUID-28D86779-8D2A-4741-8D78-49830EFF9473" name="GUID-28D86779-8D2A-4741-8D78-49830EFF9473"></a><h4 id="JSSEC-GUID-28D86779-8D2A-4741-8D78-49830EFF9473" class="sect4">Validating an XML Signature</h4>
<div><p></p>
<p>This example shows you how to validate an XML Signature using the Java XML Digital Signature API. The example uses DOM (the Document Object Model) to parse an XML document containing a Signature element and a DOM implementation to validate the signature.</p>
</div>
</div>
<div class="sect4"><a id="GUID-B2651FD1-F5CD-49D1-8541-466ABAB7ECA8" name="GUID-B2651FD1-F5CD-49D1-8541-466ABAB7ECA8"></a><h4 id="JSSEC-GUID-B2651FD1-F5CD-49D1-8541-466ABAB7ECA8" class="sect4">Instantiating the Document that Contains the Signature</h4>
<div><p></p>
<p>First we use a JAXP <span class="apiname">DocumentBuilderFactory</span> to parse the XML document containing the <span class="apiname">Signature</span>. An application obtains the default implementation for <span class="apiname">DocumentBuilderFactory</span> by calling the following line of code:</p>
<pre class="oac_no_warn" dir="ltr">    DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();</pre>
<p></p>
<p>We must also make the factory namespace-aware:</p>
<pre class="oac_no_warn" dir="ltr">    dbf.setNamespaceAware(true);</pre>
<p></p>
<p>Next, we use the factory to get an instance of a <span class="apiname">DocumentBuilder</span>, which is used to parse the document:</p>
<pre class="oac_no_warn" dir="ltr">    Document doc = null;
    try (FileInputStream fis = new FileInputStream(args[0])) {
        doc = dbf.newDocumentBuilder().parse(fis);
    }</pre>
</div>
</div>
<div class="sect4"><a id="GUID-66D2F1B6-2D1E-4721-B70B-4BA32103A79E" name="GUID-66D2F1B6-2D1E-4721-B70B-4BA32103A79E"></a><h4 id="JSSEC-GUID-66D2F1B6-2D1E-4721-B70B-4BA32103A79E" class="sect4">Specifying the Signature Element to be Validated</h4>
<div><p></p>
<p>We need to specify the <span class="apiname">Signature</span> element that we want to validate, since there could be more than one in the document. We use the DOM method <span class="apiname">Document.getElementsByTagNameNS</span>, passing it the XML Signature namespace URI and the tag name of the <span class="apiname">Signature</span> element, as shown:</p>
<pre class="oac_no_warn" dir="ltr">    NodeList nl =
        doc.getElementsByTagNameNS(XMLSignature.XMLNS, "Signature");
    if (nl.getLength() == 0) {
        throw new Exception("Cannot find Signature element");
    } </pre>
<p>This returns a list of all <span class="apiname">Signature</span> elements in the document. In this example, there is only one <span class="apiname">Signature</span> element.</p>
</div>
</div>
<div class="sect4"><a id="GUID-FCBFE214-3F87-412D-BC0F-EC4CE1519529" name="GUID-FCBFE214-3F87-412D-BC0F-EC4CE1519529"></a><h4 id="JSSEC-GUID-FCBFE214-3F87-412D-BC0F-EC4CE1519529" class="sect4">Creating a Validation Context</h4>
<div><p></p>
<p>We create an <span class="apiname">XMLValidateContext</span> instance containing input parameters for validating the signature. Since we are using DOM, we instantiate a <span class="apiname">DOMValidateContext</span> instance (a subclass of <span class="apiname">XMLValidateContext</span>), and pass it two parameters, a <span class="apiname">KeyValueKeySelector</span> object and a reference to the Signature element to be validated (which is the first entry of the <span class="apiname">NodeList</span> we generated earlier):</p>
<pre class="oac_no_warn" dir="ltr">    DOMValidateContext valContext = new DOMValidateContext
        (new KeyValueKeySelector(), nl.item(0));</pre>
<p>The <span class="apiname">KeyValueKeySelector</span> is explained in greater detail in <a href="java-xml-digital-signature-api-overview-and-tutorial.htm#GUID-26946ED1-1BBE-4AFD-B1CA-5A6A46FD7354">Using KeySelectors</a>.</p>
</div>
</div>
<div class="sect4"><a id="GUID-B5297B69-8989-4D40-994D-C40ED0C71C94" name="GUID-B5297B69-8989-4D40-994D-C40ED0C71C94"></a><h4 id="JSSEC-GUID-B5297B69-8989-4D40-994D-C40ED0C71C94" class="sect4">Unmarshalling the XML Signature</h4>
<div><p></p>
<p>We extract the contents of the <span class="apiname">Signature</span> element into an <span class="apiname">XMLSignature</span> object. This process is called unmarshalling. The <span class="apiname">Signature</span> element is unmarshalled using an <span class="apiname">XMLSignatureFactory</span> object. An application can obtain a DOM implementation of <span class="apiname">XMLSignatureFactory</span> by calling the following line of code:</p>
<pre class="oac_no_warn" dir="ltr">    XMLSignatureFactory fac = XMLSignatureFactory.getInstance("DOM");</pre>
<p>We then invoke the <span class="apiname">unmarshalXMLSignature</span> method of the factory to unmarshal an <span class="apiname">XMLSignature</span> object, and pass it the validation context we created earlier:</p>
<pre class="oac_no_warn" dir="ltr">    XMLSignature signature = fac.unmarshalXMLSignature(valContext);</pre>
</div>
</div>
<div class="sect4"><a id="GUID-CF8C37C4-7360-4833-83FB-6A2948C26818" name="GUID-CF8C37C4-7360-4833-83FB-6A2948C26818"></a><h4 id="JSSEC-GUID-CF8C37C4-7360-4833-83FB-6A2948C26818" class="sect4">Validating the XML Signature</h4>
<div><p></p>
<p>Now we are ready to validate the signature. We do this by invoking the validate method on the <span class="apiname">XMLSignature</span> object, and pass it the validation context as follows:</p>
<pre class="oac_no_warn" dir="ltr">    boolean coreValidity = signature.validate(valContext);</pre>
<p>The validate method returns "true" if the signature validates successfully according to the core validation rules in the W3C XML Signature Recommendation, and false otherwise.</p>
</div>
<div class="sect5"><a id="GUID-20CF389E-3F3F-4156-B8A3-CFB411E75274" name="GUID-20CF389E-3F3F-4156-B8A3-CFB411E75274"></a><h5 id="JSSEC-GUID-20CF389E-3F3F-4156-B8A3-CFB411E75274" class="sect5">What If the XML Signature Fails to Validate?</h5>
<div><p></p>
<p>If the <span class="apiname">XMLSignature.validate</span> method returns false, we can try to narrow down the cause of the failure. There are two phases in core XML Signature validation:</p>
<ul style="list-style-type: disc;"><li>Signature validation (the cryptographic verification of the signature)</li>
<li>Reference validation (the verification of the digest of each reference in the signature)</li>
</ul>
<p>Each phase must be successful for the signature to be valid. To check if the signature failed to cryptographically validate, we can check the status, as follows:</p>
<pre class="oac_no_warn" dir="ltr">    boolean sv = signature.getSignatureValue().validate(valContext);
    System.out.println("signature validation status: " + sv);</pre>
<p>We can also iterate over the references and check the validation status of each one, as follows:</p>
<pre class="oac_no_warn" dir="ltr">    Iterator&lt;Reference&gt; i =
        signature.getSignedInfo().getReferences().iterator();
    for (int j=0; i.hasNext(); j++) {
        boolean refValid = i.next().validate(valContext);
        System.out.println("ref["+j+"] validity status: " + refValid);
    }</pre>
</div>
</div>
</div>
<div class="sect4"><a id="GUID-26946ED1-1BBE-4AFD-B1CA-5A6A46FD7354" name="GUID-26946ED1-1BBE-4AFD-B1CA-5A6A46FD7354"></a><h4 id="JSSEC-GUID-26946ED1-1BBE-4AFD-B1CA-5A6A46FD7354" class="sect4">Using KeySelectors</h4>
<div><p></p>
<p><span class="apiname">KeySelector</span>s are used to find and select keys that are needed to validate an <span class="apiname">XMLSignature</span>. Earlier, when we created a <span class="apiname">DOMValidateContext</span> object, we passed a <code class="codeph">KeyValueKeySelector</code> object as the first argument:</p>
<pre class="oac_no_warn" dir="ltr">    DOMValidateContext valContext = new DOMValidateContext
        (new KeyValueKeySelector(), nl.item(0));</pre>
<p></p>
<p>Alternatively, we could have passed a <span class="apiname">PublicKey</span> as the first argument if we already knew what key is needed to validate the signature. However, we often don't know.</p>
<p>The <code class="codeph">KeyValueKeySelector</code> class is a concrete implementation of the abstract <span class="apiname">KeySelector</span> class. The <code class="codeph">KeyValueKeySelector</code> implementation tries to find an appropriate validation key using the data contained in <span class="apiname">KeyValue</span> elements of the <span class="apiname">KeyInfo</span> element of an <span class="apiname">XMLSignature</span>. It does not determine if the key is trusted. This is a very simple <span class="apiname">KeySelector</span> implementation, designed for illustration rather than real-world usage. A more practical example of a <span class="apiname">KeySelector</span> is one that searches a <span class="apiname">KeyStore</span> for trusted keys that match <span class="apiname">X509Data</span> information (for example, <span class="apiname">X509SubjectName</span>, <span class="apiname">X509IssuerSerial</span>, <span class="apiname">X509SKI</span>, or <span class="apiname">X509Certificate</span> elements) contained in a <span class="apiname">KeyInfo</span>.</p>
<p>The implementation of the <code class="codeph">KeyValueKeySelector</code> class is as follows:</p>
<pre class="oac_no_warn" dir="ltr">    private static class KeyValueKeySelector extends KeySelector {
        public KeySelectorResult select(KeyInfo keyInfo,
                                        KeySelector.Purpose purpose,
                                        AlgorithmMethod method,
                                        XMLCryptoContext context)
            throws KeySelectorException {
            if (keyInfo == null) {
                throw new KeySelectorException("Null KeyInfo object!");
            }
            SignatureMethod sm = (SignatureMethod) method;
            List&lt;XMLStructure&gt; list = keyInfo.getContent();

            for (int i = 0; i &lt; list.size(); i++) {
                XMLStructure xmlStructure = list.get(i);
                if (xmlStructure instanceof KeyValue) {
                    PublicKey pk = null;
                    try {
                        pk = ((KeyValue)xmlStructure).getPublicKey();
                    } catch (KeyException ke) {
                        throw new KeySelectorException(ke);
                    }
                    // make sure algorithm is compatible with method
                    if (algEquals(sm.getAlgorithm(), pk.getAlgorithm())) {
                        return new SimpleKeySelectorResult(pk);
                    }
                }
            }
            throw new KeySelectorException("No KeyValue element found!");
        }

        static boolean algEquals(String algURI, String algName) {
            if (algName.equalsIgnoreCase("DSA") &amp;&amp;
                algURI.equalsIgnoreCase("http://www.w3.org/2009/xmldsig11#dsa-sha256")) {
                return true;
            } else if (algName.equalsIgnoreCase("RSA") &amp;&amp;
                       algURI.equalsIgnoreCase("http://www.w3.org/2001/04/xmldsig-more#rsa-sha256")) {
                return true;
            } else {
                return false;
            }
        }
    }

    private static class SimpleKeySelectorResult implements KeySelectorResult {
        private PublicKey pk;
        SimpleKeySelectorResult(PublicKey pk) {
            this.pk = pk;
        }

        public Key getKey() { return pk; }
    }</pre>
</div>
</div>
</div>
<div class="sect3"><a id="GUID-1152D2A5-ECBB-4727-9B0F-1941E4171108" name="GUID-1152D2A5-ECBB-4727-9B0F-1941E4171108"></a><h3 id="JSSEC-GUID-1152D2A5-ECBB-4727-9B0F-1941E4171108" class="sect3">GenEnveloped Example</h3>
<div><p></p>
<p>To compile and run this sample, execute the following command:</p>
<pre class="oac_no_warn" dir="ltr">$ javac GenEnveloped.java
$ java GenEnveloped envelope.xml envelopedSignature.xml</pre>
<p>The sample program will generate an enveloped signature of the document in the file <code>envelope.xml</code> and store it in the file <code>envelopedSignature.xml</code> in the current working directory.</p>
<div class="example" id="GUID-1152D2A5-ECBB-4727-9B0F-1941E4171108__GUID-6CB4162E-30CE-41BF-8767-2C5B88063D8F"><p class="titleinexample">Example 12-4 GenEnveloped.java</p><pre class="oac_no_warn" dir="ltr">import javax.xml.crypto.dsig.*;
import javax.xml.crypto.dsig.dom.DOMSignContext;
import javax.xml.crypto.dsig.keyinfo.*;
import javax.xml.crypto.dsig.spec.*;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.OutputStream;
import java.security.*;
import java.util.List;
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.transform.*;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;
import org.w3c.dom.Document;

/**
 * This is a simple example of generating an Enveloped XML
 * Signature using the Java XML Digital Signature API. The
 * resulting signature will look like (key and signature
 * values will be different):
 *
 * &lt;pre&gt;&lt;code&gt;
 *&lt;Envelope xmlns="urn:envelope"&gt;
 * &lt;Signature xmlns="http://www.w3.org/2000/09/xmldsig#"&gt;
 *   &lt;SignedInfo&gt;
 *     &lt;CanonicalizationMethod Algorithm="http://www.w3.org/TR/2001/REC-xml-c14n-20010315"/&gt;
 *     &lt;SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"/&gt;
 *     &lt;Reference URI=""&gt;
 *       &lt;Transforms&gt;
 *         &lt;Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/&gt;
 *       &lt;/Transforms&gt;
 *       &lt;DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256"/&gt;
 *       &lt;DigestValue&gt;/juoQ4bDxElf1M+KJauO20euW+QAvvPP0nDCruCQooM=&lt;DigestValue&gt;
 *     &lt;/Reference&gt;
 *   &lt;/SignedInfo&gt;
 *   &lt;SignatureValue&gt;
 *     YeS+F0uiYv0h946M69Q9pKFNnD6dxUwLA8QT3GX/0H3cSPKRnNFyZiR4RPgaA1ir/ztb4rt6Lqb8
 *     hgwPERIa5qhoGUJyHDfUTcQ0Xqn1jYCVoC3ho+oUgJPXNVgtMAtpvOgxcWXUPATYdyimO6RrHF8+
 *     JXDkeICI9BPA4NKN1i77CAy6JJbaA87aNIpMJPImwJf8CM7mYsXremZz+RsafNE2cXXRzAoNOynC
 *     pi4oPYpE7CBLzhd23gf7zYRoyT06/bVIj4j3qOlVY1TQofsQ20NtAz6PbqAs7QkNoDzkX1CYlDSJ
 *     U8cGHuwXpul/UIpOiL6MZF8I/YI4ZlJn+O8Mvg==
 *   &lt;/SignatureValue&gt;
 *   &lt;KeyInfo&gt;
 *     &lt;KeyValue&gt;
 *       &lt;RSAKeyValue&gt;
 *         &lt;Modulus&gt;
 *           mH0S/iw2K2tFTFHI75BtB67pzjR52HvQ8K7Xi5UX3NJm0oA+KX2mm0IrVcUuv609vbAAyQoW7CWm
 *           4kswVgStCm68dlw36309cxrEmPhG+PKBmUaGuBmRzwityjXRyRZJ6yaLenE8SJO/DC5ntQvmHqQQ
 *           qeOJYvz2Cbi2bi6x9XwmpqOfZCE5iTvYwioEsrglhP1uLG9fiXyNR2PXUTyLqD91HLhZFj1CEiU7
 *           aE++WfkKaowIx5p8e3F6hQ+VFRNXjtemK5aajuL0gwU+Oujg9ijgbyMh19vBoI8LruJoMOBrYFNN
 *           2boQJ3wP0Ek7CPIqAzQB5MnmvKc9jICKiiZVZw==
 *         &lt;/Modulus&gt;
 *         &lt;Exponent&gt;AQAB&lt;/Exponent&gt;
 *       &lt;/RSAKeyValue&gt;
 *     &lt;/KeyValue&gt;
 *   &lt;/KeyInfo&gt;
 * &lt;/Signature&gt;
 *&lt;/Envelope&gt;
 * &lt;/code&gt;&lt;/pre&gt;
 */
public class GenEnveloped {

    //
    // Synopsis: java GenEnveloped [document] [output]
    //
    //    where "document" is the name of a file containing the XML document
    //    to be signed, and "output" is the name of the file to store the
    //    signed document. The 2nd argument is optional - if not specified,
    //    standard output will be used.
    //
    public static void main(String[] args) throws Exception {
    	
        // Instantiate the document to be signed
        DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
        dbf.setNamespaceAware(true);
        Document doc = null;
        try (FileInputStream fis = new FileInputStream(args[0])) {
            doc = dbf.newDocumentBuilder().parse(fis);
        }
        
        // Create a RSA KeyPair
        KeyPairGenerator kpg = KeyPairGenerator.getInstance("RSA");
        kpg.initialize(2048);
        KeyPair kp = kpg.generateKeyPair();
        
        // Create a DOMSignContext and specify the RSA PrivateKey and
        // location of the resulting XMLSignature's parent element
        DOMSignContext dsc = new DOMSignContext
            (kp.getPrivate(), doc.getDocumentElement());
      
        // Create a DOM XMLSignatureFactory that will be used to generate the
        // enveloped signature
        XMLSignatureFactory fac = XMLSignatureFactory.getInstance("DOM");

        // Create a Reference to the enveloped document (in this case we are
        // signing the whole document, so a URI of "" signifies that) and
        // also specify the SHA256 digest algorithm and the ENVELOPED Transform.
        Reference ref = fac.newReference
            ("", fac.newDigestMethod(DigestMethod.SHA256, null),
             List.of
              (fac.newTransform
                (Transform.ENVELOPED, (TransformParameterSpec) null)),
             null, null);

        // Create the SignedInfo
        SignedInfo si = fac.newSignedInfo
            (fac.newCanonicalizationMethod
             (CanonicalizationMethod.INCLUSIVE_WITH_COMMENTS,
              (C14NMethodParameterSpec) null),
             fac.newSignatureMethod("http://www.w3.org/2001/04/xmldsig-more#rsa-sha256", null),
             List.of(ref));

        // Create a KeyValue containing the RSA PublicKey that was generated
        KeyInfoFactory kif = fac.getKeyInfoFactory();
        KeyValue kv = kif.newKeyValue(kp.getPublic());

        // Create a KeyInfo and add the KeyValue to it
        KeyInfo ki = kif.newKeyInfo(List.of(kv));

        // Create the XMLSignature (but don't sign it yet)
        XMLSignature signature = fac.newXMLSignature(si, ki);

        // Marshal, generate (and sign) the enveloped signature
        signature.sign(dsc);

        // output the resulting document
        OutputStream os;
        if (args.length &gt; 1) {
           os = new FileOutputStream(args[1]);
        } else {
           os = System.out;
        }

        TransformerFactory tf = TransformerFactory.newInstance();
        Transformer trans = tf.newTransformer();
        trans.transform(new DOMSource(doc), new StreamResult(os));
    }
}</pre>
</div>
<!-- class="example" -->
<div class="example" id="GUID-1152D2A5-ECBB-4727-9B0F-1941E4171108__GUID-EB71567E-2E84-4301-98EC-65664665A996"><p class="titleinexample">Example 12-5 envelope.xml</p><pre class="oac_no_warn" dir="ltr">&lt;Envelope xmlns="urn:envelope"&gt;
&lt;/Envelope&gt;
</pre>
</div>
<!-- class="example" -->
</div>
<div class="sect4"><a id="GUID-177088CC-2CFD-477D-BB05-E8B9C48AE270" name="GUID-177088CC-2CFD-477D-BB05-E8B9C48AE270"></a><h4 id="JSSEC-GUID-177088CC-2CFD-477D-BB05-E8B9C48AE270" class="sect4">Generating an XML Signature</h4>
<div><p></p>
<p>This example shows you how to generate an XML Signature using the XML Digital Signature API. More specifically, the example generates an enveloped XML Signature of an XML document. An enveloped signature is a signature that is contained inside the content that it is signing. The example uses DOM (the Document Object Model) to parse the XML document to be signed and a DOM implementation to generate the resulting signature.</p>
<p>A basic knowledge of XML Signatures and their different components is helpful for understanding this section. See <a href="https://www.w3.org/TR/xmldsig-core/" target="_blank">XML Signature Syntax and Processing Version 1.1</a> for more information.</p>
</div>
</div>
<div class="sect4"><a id="GUID-37E2785A-6ACD-4E09-9A72-4F6AE9A641D9" name="GUID-37E2785A-6ACD-4E09-9A72-4F6AE9A641D9"></a><h4 id="JSSEC-GUID-37E2785A-6ACD-4E09-9A72-4F6AE9A641D9" class="sect4">Instantiating the Document to be Signed</h4>
<div><p></p>
<p>First, we use a JAXP <span class="apiname">DocumentBuilderFactory</span> to parse the XML document that we want to sign. An application obtains the default implementation for <span class="apiname">DocumentBuilderFactory</span> by calling the following line of code:</p>
<pre class="oac_no_warn" dir="ltr">    DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();</pre>
<p>We must also make the factory namespace-aware:</p>
<pre class="oac_no_warn" dir="ltr">    dbf.setNamespaceAware(true);</pre>
<p>Next, we use the factory to get an instance of a <span class="apiname">DocumentBuilder</span>, which is used to parse the document:</p>
<pre class="oac_no_warn" dir="ltr">    Document doc = null;
    try (FileInputStream fis = new FileInputStream(args[0])) {
        doc = dbf.newDocumentBuilder().parse(fis);
    }</pre>
</div>
</div>
<div class="sect4"><a id="GUID-A0C0D616-CD13-441C-A1A2-122431692B9F" name="GUID-A0C0D616-CD13-441C-A1A2-122431692B9F"></a><h4 id="JSSEC-GUID-A0C0D616-CD13-441C-A1A2-122431692B9F" class="sect4">Creating a Public Key Pair</h4>
<div><p></p>
<p>We generate a public key pair. Later in the example, we will use the private key to generate the signature. We create the key pair with a <span class="apiname">KeyPairGenerator</span>. In this example, we will create a RSA <span class="apiname">KeyPair</span> with a length of 2048 bytes:</p>
<pre class="oac_no_warn" dir="ltr">    KeyPairGenerator kpg = KeyPairGenerator.getInstance("RSA");
    kpg.initialize(2048);
    KeyPair kp = kpg.generateKeyPair();</pre>
<p>In practice, the private key is usually previously generated and stored in a <span class="apiname">KeyStore</span> file with an associated public key certificate.</p>
</div>
</div>
<div class="sect4"><a id="GUID-2FA5FBA6-8DB7-460D-BDEA-2BF38B14BC19" name="GUID-2FA5FBA6-8DB7-460D-BDEA-2BF38B14BC19"></a><h4 id="JSSEC-GUID-2FA5FBA6-8DB7-460D-BDEA-2BF38B14BC19" class="sect4">Creating a Signing Context</h4>
<div><p></p>
<p>We create an <span class="apiname">XMLSignContext</span> containing input parameters for generating the signature. Since we are using DOM, we instantiate a <span class="apiname">DOMSignContext</span> (a subclass of <span class="apiname">XMLSignContext</span>), and pass it two parameters, the private key that will be used to sign the document and the root of the document to be signed:</p>
<pre class="oac_no_warn" dir="ltr">    DOMSignContext dsc = new DOMSignContext
        (kp.getPrivate(), doc.getDocumentElement());</pre>
</div>
</div>
<div class="sect4"><a id="GUID-3DEB54D1-220A-4140-832D-DD42976057B6" name="GUID-3DEB54D1-220A-4140-832D-DD42976057B6"></a><h4 id="JSSEC-GUID-3DEB54D1-220A-4140-832D-DD42976057B6" class="sect4">Assembling the XML Signature</h4>
<div><p></p>
<p>We assemble the different parts of the Signature element into an <span class="apiname">XMLSignature</span> object. These objects are all created and assembled using an <span class="apiname">XMLSignatureFactory</span> object. An application obtains a DOM implementation of <span class="apiname">XMLSignatureFactory</span> by calling the following line of code:</p>
<pre class="oac_no_warn" dir="ltr">    XMLSignatureFactory fac = XMLSignatureFactory.getInstance("DOM");</pre>
<p>We then invoke various factory methods to create the different parts of the <span class="apiname">XMLSignature</span> object as shown below. We create a <span class="apiname">Reference</span> object, passing to it the following:</p>
<ul style="list-style-type: disc;"><li><p>The URI of the object to be signed (We specify a URI of "", which implies the root of the document.)</p>
</li>
</ul>
<ul style="list-style-type: disc;"><li><p>The <span class="apiname">DigestMethod</span> (we use SHA256)</p>
</li>
</ul>
<ul style="list-style-type: disc;"><li><p>A single <span class="apiname">Transform</span>, the enveloped <span class="apiname">Transform</span>, which is required for enveloped signatures so that the signature itself is removed before calculating the signature value</p>
</li>
</ul>
<pre class="oac_no_warn" dir="ltr">    Reference ref = fac.newReference
        ("", fac.newDigestMethod(DigestMethod.SHA256, null),
         List.of
          (fac.newTransform
            (Transform.ENVELOPED, (TransformParameterSpec) null)),
         null, null);</pre>
<p>Next, we create the <span class="apiname">SignedInfo</span> object, which is the object that is actually signed, as shown below. When creating the <span class="apiname">SignedInfo</span>, we pass as parameters:</p>
<ul style="list-style-type: disc;"><li><p>The <span class="apiname">CanonicalizationMethod</span> (we use inclusive and preserve comments)</p>
</li>
</ul>
<ul style="list-style-type: disc;"><li><p>The <span class="apiname">SignatureMethod</span> (we use RSA)</p>
</li>
</ul>
<ul style="list-style-type: disc;"><li><p>A list of <span class="apiname">References</span> (in this case, only one)</p>
</li>
</ul>
<pre class="oac_no_warn" dir="ltr">    SignedInfo si = fac.newSignedInfo
        (fac.newCanonicalizationMethod
         (CanonicalizationMethod.INCLUSIVE_WITH_COMMENTS,
          (C14NMethodParameterSpec) null),
         fac.newSignatureMethod("http://www.w3.org/2001/04/xmldsig-more#rsa-sha256", null),
         List.of(ref));</pre>
<p>Next, we create the optional <span class="apiname">KeyInfo</span> object, which contains information that enables the recipient to find the key needed to validate the signature. In this example, we add a <span class="apiname">KeyValue</span> object containing the public key. To create <span class="apiname">KeyInfo</span> and its various subtypes, we use a <span class="apiname">KeyInfoFactory</span> object, which can be obtained by invoking the <span class="apiname">getKeyInfoFactory</span> method of the <span class="italic">XMLSignatureFactory</span>, as follows:</p>
<pre class="oac_no_warn" dir="ltr">    KeyInfoFactory kif = fac.getKeyInfoFactory();</pre>
<p>We then use the <span class="apiname">KeyInfoFactory</span> to create the <span class="apiname">KeyValue</span> object and add it to a <span class="apiname">KeyInfo</span> object:</p>
<pre class="oac_no_warn" dir="ltr">    KeyValue kv = kif.newKeyValue(kp.getPublic());
    KeyInfo ki = kif.newKeyInfo(List.of(kv));</pre>
<p>Finally, we create the <span class="apiname">XMLSignature</span> object, passing as parameters the <span class="apiname">SignedInfo</span> and <span class="apiname">KeyInfo</span> objects that we created earlier:</p>
<pre class="oac_no_warn" dir="ltr">    XMLSignature signature = fac.newXMLSignature(si, ki);</pre>
<p>Notice that we haven't actually generated the signature yet; we'll do that in the next step.</p>
</div>
</div>
<div class="sect4"><a id="GUID-3B6E8DE8-AC10-46B2-BC89-9E0B2CE8634C" name="GUID-3B6E8DE8-AC10-46B2-BC89-9E0B2CE8634C"></a><h4 id="JSSEC-GUID-3B6E8DE8-AC10-46B2-BC89-9E0B2CE8634C" class="sect4">Generating the XML Signature</h4>
<div><p></p>
<p>Now we are ready to generate the signature, which we do by invoking the sign method on the <span class="apiname">XMLSignature</span> object, and pass it the signing context as follows:</p>
<pre class="oac_no_warn" dir="ltr">    signature.sign(dsc);</pre>
<p></p>
<p>The resulting document now contains a signature, which has been inserted as the last child element of the root element.</p>
</div>
</div>
<div class="sect4"><a id="GUID-1D6C3745-9E04-400A-ADD1-65E5FD3ADB5C" name="GUID-1D6C3745-9E04-400A-ADD1-65E5FD3ADB5C"></a><h4 id="JSSEC-GUID-1D6C3745-9E04-400A-ADD1-65E5FD3ADB5C" class="sect4">Printing or Displaying the Resulting Document</h4>
<div><p></p>
<p>You can use the following code to print the resulting signed document to a file or standard output:</p>
<pre class="oac_no_warn" dir="ltr">    OutputStream os;
    if (args.length &gt; 1) {
       os = new FileOutputStream(args[1]);
    } else {
       os = System.out;
    }

    TransformerFactory tf = TransformerFactory.newInstance();
    Transformer trans = tf.newTransformer();
    trans.transform(new DOMSource(doc), new StreamResult(os));</pre>
<p></p>
</div>
</div>
</div>
</div>
</div><!-- class="ind" --><!-- Start Footer -->
<div class="footer">
<hr />
<table class="simple oac_no_warn" summary="" cellspacing="0" cellpadding="0" width="100%">
<col width="33%" />
<col width="*" />
<col width="33%" />
<tr>
<td valign="bottom">
<table class="simple oac_no_warn" summary="" cellspacing="0" cellpadding="0" width="100">
<tr>
<td align="center">
<a href="java-sasl-api-programming-and-deployment-guide1.htm">
<img src="../../dcommon/gifs/leftnav.gif" alt="Previous" /><br />
<span class="icon">Previous</span>
</a>
</td>
<td align="center">
<a href="security-api-specification1.htm">
<img src="../../dcommon/gifs/rightnav.gif" alt="Next" /><br />
<span class="icon">Next</span>
</a>
</td>
<td> </td>
</tr>
</table>
</td>
<td class="copyrightlogo">
<img class="copyrightlogo" src="../../dcommon/gifs/oracle.gif" alt="Oracle Logo" />
<a href="../../dcommon/html/cpyr.htm"><br />
<span class="copyrightlogo">Copyright&nbsp;&copy;&nbsp;1993, 2018, Oracle&nbsp;and/or&nbsp;its&nbsp;affiliates.&nbsp;All&nbsp;rights&nbsp;reserved.</span></a>
</td>
<td valign="bottom" align="right">
<table class="simple oac_no_warn" summary="" cellspacing="0" cellpadding="0" width="225">
<tr>
<td>
 
</td>
<td align="center" valign="top">
<a href="toc.htm"><img src="../../dcommon/gifs/toc.gif" alt="Go To Table Of Contents" /><br />
<span class="icon">Contents</span></a>
</td>
</tr>
</table>
</td>
</tr>
</table>

</div>
<!-- class="footer" -->
</body>

