# Created by: ijliao
# $FreeBSD$

PORTNAME=	socat
PORTVERSION=	1.7.3.1
PORTREVISION=	0
CATEGORIES=	net ipv6
MASTER_SITES=	http://www.dest-unreach.org/socat/download/ \
		LOCAL/ehaupt

MAINTAINER=	ehaupt@FreeBSD.org
COMMENT=	Multipurpose relay and more

LICENSE=	GPLv2

USES=		compiler cpe ssl tar:bzip2
GNU_CONFIGURE=	yes
USE_RC_SUBR=	socat

CPE_VENDOR=	dest-unreach

PORTSCOUT=	skipv:2.0.0-b2

PLIST_FILES=	bin/filan bin/procan bin/socat man/man1/socat.1.gz
PORTDOCS=	EXAMPLES README SECURITY FAQ

OPTIONS_DEFINE=	DOCS

.include <bsd.port.pre.mk>

.if ${SSL_DEFAULT} != base
.if ${SSL_DEFAULT:Mopenssl-devel}
BROKEN=		Does not build with openssl-devel
.endif
CFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
.endif

.if ${COMPILER_TYPE} == "clang"
CFLAGS+=	-Wno-unused-comparison
.endif

do-install:
.for f in filan procan socat
	${INSTALL_PROGRAM} ${WRKSRC}/${f} ${STAGEDIR}${PREFIX}/bin
.endfor
	${INSTALL_MAN} ${WRKSRC}/doc/${PORTNAME}.1 ${STAGEDIR}${MAN1PREFIX}/man/man1
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	cd ${WRKSRC} && ${INSTALL_DATA} ${PORTDOCS} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.post.mk>
