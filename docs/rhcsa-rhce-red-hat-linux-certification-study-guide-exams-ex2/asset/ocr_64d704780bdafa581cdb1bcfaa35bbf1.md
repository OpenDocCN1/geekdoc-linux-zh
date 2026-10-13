# FIGURE 12-2

A newpackage.
spec file.

```
Name:
Version:
Release: 1%{?dist}
Summary:
Group:
License:
URL:
Source0:
BuildRoot: %{_tmppath}/%{name}-%{version}-%{release}-root-%{__id_u} .
)
BuildRequires:
Requires:
%description

%prep
%setup -q

%build
%configure
make %{?_smp_mflags}

%install
rm -rf $RPM_BUILD_ROOT
make install DESTDIR=$RPM_BUILD_ROOT

%clean
rm -rf $RPM_BUILD_ROOT

%files
%defattr(-,root,root,)
%doc
*newpackage.spec* 42L, 488C
```

Open-source software may be released under a variety of different licenses. Most RHEL 6 software is released under the GPL.

License: McGraw-Hill

You can either comment out the URL, or add an appropriate address, as shown here:

URL: http://www.mheducation.com/

The Source0 is perhaps most important. It specifies the name of the gzip compressed tar archive file, either from a remote URL, or from the local rpmbuild/SOURCES